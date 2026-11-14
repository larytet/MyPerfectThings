# AST-Mutation Agents and Meaning-Level Review

## Background

Code is stored and diffed as text. A parser turns it into an Abstract Syntax Tree (AST): "function -> parameters -> body -> if -> call". An AST-mutation agent edits that tree through tools (add node, delete node, rename symbol everywhere, wrap call in error handling) and prints it back as source.

Attractive because:
- The output parses by construction, so no missing braces.
- Large refactors become mechanical, such as renaming a function in 400 files without touching strings or comments.

The cost shows up in review. Git diffs compare lines, not meaning. A tool that regenerates code from a tree can reformat, reorder imports or move a function. That is a big text change and a tiny logical one. The PR shows thousands of red and green lines for one semantic change, and the reviewer cannot tell which lines matter.

## How much to believe

- The mechanism is real. AST rewriting tools are established: tree-sitter, ast-grep, jscodeshift, OpenRewrite, Comby.
- Most mainstream coding agents still use search-and-replace text edits, which give normal readable diffs. Research and small tools for AST-level agent actions are appearing (below), but they are not the default.
- "Developers are being forced to abandon Git diffs" is an opinion from the source video, with no evidence found.
- The practical point holds: the more structural and automated the edits, the more review needs to show meaning, not lines.

## Existing pieces (as of 2026-11)

Search results are mostly vendor pages and launch listings. Treat claims as unverified unless marked as a paper.

### Agents that edit the tree

| Item | What it does | Notes |
|---|---|---|
| [CodeStruct](https://arxiv.org/pdf/2604.05407) (ACL 2026, AWS AI Labs) | Repo as an AST action space. `readCode` / `editCode` act on named program entities, not string matches or line numbers. | Paper reports +1.2-5.0% Pass@1 on SWE-Bench Verified across six LLMs and 12-38% fewer tokens for most models. Edits with syntax errors are rejected after parsing, so validity is checked, not guaranteed by generation. |
| [To Diff or Not to Diff?](https://arxiv.org/pdf/2604.27296) (arXiv, Apr 2026) | BlockDiff and FuncDiff express changes as rewrites of AST-derived blocks. AdaEdit picks between diff and full-code output. | Reports similar accuracy to full generation with over 30% lower latency and cost on long-code edits. |
| [AST-FIM](https://arxiv.org/pdf/2506.00204v1) | Pretraining that masks whole AST subtrees so a model fills complete syntactic units. | Training method, not an agent. Related idea. |
| [agent-file-tools (AFT)](https://docs.rs/crate/agent-file-tools/0.3.0/source/README.md) | Tree-sitter toolkit for agents: outline, symbol-addressed edits, transactional batches, ast-grep pattern search and replace. | Claims symbol addressing avoids line-shift breakage. |
| [FastEdit](https://pypi.org/project/fastedits/0.4.1/) | Tree-sitter locates a function or class by name, model writes only the change. | Claims 44-54% fewer output tokens. Self-reported, no independent benchmark found. |

### Tools that diff the tree

- [difftastic](https://github.com/Wilfred/difftastic): CLI structural diff on tree-sitter parse trees, ignores formatting-only changes. [Walkthrough for reviewing AI code](https://blog.openreplay.com/review-ai-generated-code-difftastic/).
- [GumTree](https://github.com/GumTreeDiff/gumtree): research-grade AST differ that detects moved, renamed and updated nodes.
- [SemanticDiff](https://semanticdiff.com): VS Code extension and GitHub app that hides moves and reformatting in PR review. Limited language set.
- JetBrains IDEs: some structure-aware diffing, such as move detection.

### Review products aimed at agent-written PRs

- [CodeRabbit Semantic Diff](https://coderabbit.ai/blog/introducing-semantic-diff): groups related movement and token-level changes. Its own post calls this a presentation layer and says its review engine goes further. Also [Change Stack](https://www.coderabbit.ai/blog/introducing-change-stack-the-first-ai-native-code-review-interface).
- [Diffcore](https://understandingdata.com/tools/diffcore/): CLI and desktop tool that clusters related file changes into review units ordered by data flow, aimed at agent handoffs.
- [Semantic Diffs by Plane](https://plane.so/semantic-diffs-by-plane), [Seendiff](https://aiindigo.com/tool/seendiff) (LLM summary of what and why), [Diffen.ai](https://www.producthunt.com/products/diffen-ai/launches) (reviews PRs, fixes on a branch, runs tests; launched 2026-02-18), [Superdiffs](https://index.dodopayments.com/superdiffs).
- Funded AI reviewers per a [2026 roundup](https://composio.dev/blog/best-ai-powered-code-review-tools-in-2026): CodeRabbit, Greptile, Qodo (built on open-source PR-Agent).
- [Baz on advanced diffing and parsing for an AI review agent](https://baz.co/resources/building-an-ai-code-review-agent-advanced-diffing-parsing-and-agentic-workflows).

## What is not covered

Structural diffs say "this function moved", "rename only", "formatting only". None found says "this PR now allows shipping before payment". They do not know intent or domain rules. Coverage is also per-language, so a polyglot repo falls back to line diffs.

Nobody found closes the loop between the agent's edit and the review. The agent knows which operations it applied (rename X to Y, wrap call Z). That log is exact, and review tools throw it away and reconstruct it from before/after text.

## The Idea

Two linked parts.

1. **Edit-log as the diff.** An AST-mutation agent emits a typed operation log alongside the code: `rename(sym, new)`, `move(fn, file)`, `wrap(call, try/catch)`, `add_check(fn, cond)`. The PR carries the log as the primary review artifact: "1 rename across 400 files, 1 move, 2 behavior changes". The reviewer approves the mechanical operations in one click and reads only the behavior-changing ones. The text diff stays available as a fallback.
   - Verifiable: replay the log on the base commit and check the result equals the PR tree. If it does not, the log lied and the PR is flagged.
   - Behavior-changing vs behavior-preserving is the key field. Renames, moves and import reordering are preserving. A new condition, a new call or a changed default is not.

2. **Invariant check on the behavior-changing set.** Only the small residue goes to a rule layer: domain invariants written once by the team ("an order is never shipped unpaid", "every external call has a timeout"). The check asks whether any behavior-changing operation touches code covered by an invariant. This is the gap in the existing tools, and it is cheaper than reviewing the whole PR because the mechanical majority is already out of the way.

## Why it might work

- The agent already holds the structured information. Recovering it later from text is the lossy step.
- Existing differs are complementary, not rivals. difftastic or SemanticDiff can render the log; the log can be validated by replay.
- Review load is the pain. Agents open PRs continuously and humans read at human speed.

## Risks and open questions

- Mainstream agents edit text, so there is nothing to log. Option: reconstruct the log from a structural diff (GumTree-style) when the agent did not provide one, which is weaker.
- Behavior-preserving is undecidable in general. Renames can break reflection and string-keyed lookups; moves can change import side effects. The classification needs to be conservative.
- Invariants have to be written by someone. If writing them costs more than reviewing, nobody does it.
- CodeRabbit, Diffcore and others are moving toward this space and have distribution. A standalone product is exposed; an open log format that they could adopt may be the safer shape.
- Language coverage follows tree-sitter grammars.

## Cheap first test

Take 20 merged agent PRs with large diffs. Run difftastic on each and count how many changed lines are formatting or move only. If the mechanical share is under about 30 percent, the edit-log gives little. If it is over 70 percent, it is a strong signal that the review view is worth building.

## See also

- [agent-work-filing-cabinet.md](agent-work-filing-cabinet.md): provenance of agent outputs, same trust problem one layer over.
- [agent-sandbox-as-a-service.md](agent-sandbox-as-a-service.md): where such an agent would run.
