# Agent Work Filing Cabinet

## Problem

Each tool in the stack was built for something a human types or writes:

- git holds source code
- Jira holds tasks and status
- Slack holds conversation
- Notion and Confluence hold pages people write

AI work produces something none of them was designed for: evidence and knowledge in bulk - analysis, dumps, drafts, mocks, transcripts. Agents write it, and both agents and humans need to read it later. Today it lands in the working directory as untracked folders, because it has no owner.

## What is needed

1. **Somewhere to put it without thinking.** Saving an output should cost nothing, or it won't happen.
2. **Some way to find it later.** By ticket, by topic, by date. Without that, it's a dump.
3. **Some way to show it to others.** A link opens it, whether it's a report, a mock or a transcript.
4. **Some way to trust it.** Which session made it, on which code, from which data. Otherwise a number in a report can't be checked.
5. **A way for agents to use it.** A new session should be able to read what an old one produced.
6. **Ownership of both layers.** Control over how it's stored and how it's displayed - the original point about Jira, Notion and Slack.

## What is not needed

- A new collaboration suite.
- A place for code. Git already does that.
- Real-time editing.
- Anything that has to be perfect on day one.

## Where git fits

Git is one neighbor of the cabinet, not the cabinet. Only outputs that become part of the software (a doc, a fixture, a spec) belong in git. Everything else is evidence about the software, and it needs a pointer to the code, not a place inside it. That is why git+LFS feels close but not right.

## How to know it is the right one

- A session ends and the outputs are already filed, with no effort.
- A month later they are found in under a minute, and it is clear which code and session produced them.
- A link is sent to someone and it opens, with no clone and no setup.

If a solution passes those three checks, it is the right one, whatever it is built on.

## Existing pieces (as of 2026-09)

Nothing found does all of it, but four things each cover part.

| Need | Closest existing thing | What's missing |
|---|---|---|
| Publish with no thought, link that opens (2, 3) | [Agent Artifacts](https://github.com/scheemunai/agent-artifacts) - open source, self-hostable (SQLite). Agents POST markdown/HTML, get a stable versioned shareable page. | Presentation only. No ticket/topic index, provenance not a first-class field. |
| Find later (2), agents read old work (5) | [agentsview](https://github.com/kenn-io/agentsview) - local-first, full-text and semantic search over Claude Code and 20+ other agents' sessions, CLI usable by agents. SQLite archive, can push to Postgres, ClickHouse, S3. | Indexes transcripts, not the files and dumps sessions produce. No link to code version. |
| Trust (4) | [Chain-of-custody post](https://clord.dev/blog/agent-artifacts-need-chain-of-custody-2026/) proposes a metadata "passport" per artifact: run ID, model, `repo@commit`, prompt hash, tool receipts. | A schema proposal, not a product. |
| Content-addressed storage and lineage | [DVC](https://dvc.org) or lakeFS for storage; [MLflow](https://mlflow.org/docs/latest/ml/model-registry/) for run-to-code lineage. | Built for models and datasets and a data scientist's workflow - fails the "costs nothing to save" test. |

Commercial option: [Harness Artifact Registry](https://www.harness.io/products/artifact-registry) gives lineage to source commit and build pipeline, but it is enterprise CI/CD, not a place for analysis dumps.

Against the three checks: nothing files automatically at session end; agentsview gets close on transcripts but nothing joins outputs to a session and commit; Agent Artifacts passes the link check.

## The Idea

The pieces exist. The join between them doesn't. The join is a session-end hook (for example a Claude Code `Stop` hook) that:

1. gathers the session's outputs,
2. stamps them with session ID, commit, and data source,
3. files them into an artifact store with a ticket/topic index,
4. leaves the store searchable by agentsview or similar, and readable by later agents.

Ownership of both layers is realistic because Agent Artifacts and agentsview are both self-hostable.

Day-one version: a hook, an S3 bucket with a JSON sidecar per output, and a small viewer.

## Connection to other ideas

- [agent-sandbox-as-a-service.md](agent-sandbox-as-a-service.md) - the compute half. Sandboxes decide where agents run; this decides where their outputs go. A sandbox platform could file outputs on teardown.
- [signed-video-frames.md](signed-video-frames.md) - same provenance pattern: sign the output and record who made it.

## Links

- [Agent Artifacts (GitHub)](https://github.com/scheemunai/agent-artifacts)
- [Agent Artifacts Need Chain of Custody](https://clord.dev/blog/agent-artifacts-need-chain-of-custody-2026/)
- [agentsview](https://github.com/kenn-io/agentsview)
- [MLflow model registry](https://mlflow.org/docs/latest/ml/model-registry/)
- [DVC and MLflow lineage (DVC blog)](https://dvc.org/blog/end-to-end-lineage-with-dvc-and-amazon-sagemaker-ai-mlflow-apps/)
- [Harness Artifact Registry](https://www.harness.io/products/artifact-registry)
