# Diagram-to-Code Tools, Revisited With AI

## Background

In the 1990s and early 2000s a whole class of tools promised working code from a diagram plus some inline code: draw a state machine or a block diagram, type the action snippets, press Generate. Many were commercial. Some were aimed at embedded real-time systems, including avionics. Most of the general-purpose ones faded. A few narrow ones became standard and still ship code in aircraft, cars and trains.

The question here: what changes if an LLM is added to that mix, and where would it go?

## The products of that era

Facts below come from web search (2026-11) and are mostly from vendor material, Wikipedia mirrors and retrospectives. Where a point is from my own background knowledge and not from a source, it is marked (unsourced).

### Embedded and real-time (the survivors)

| Product | What it was | Details found |
|---|---|---|
| **Statemate** (I-Logix) | Statecharts tool, executable models, code generation | [I-Logix](https://en.wikipedia.org/wiki/I-Logix) was founded in Israel in 1984 as AdCad by David Harel, Amir Pnueli and the Lachover brothers. Harel's statecharts came out of consulting on avionics for the Lavi fighter. Statemate generated Ada first, then C. The team received the ACM Software System Award in 2007. Under IBM it is reported as not gaining new market, with Rhapsody as its replacement. |
| **Rhapsody** (I-Logix, later Telelogic, then IBM) | Object-oriented, UML-based, statecharts to C, C++, Ada, Java, C# | Released 1996 ([Wikipedia: I-Logix](https://en.wikipedia.org/wiki/I-Logix)). Telelogic bought I-Logix in March 2006 for about $80 million. IBM bought Telelogic on 2008-04-03. Now sold as [IBM Engineering Rhapsody](https://wiki.krisyotam.com/content/wikipedia_en_all_nopic_2026-03/Rational_Rhapsody). One source says it is still used by major automotive and aerospace/defence firms. |
| **SCADE Suite with KCG** (Esterel Technologies, from Telelogic, later ANSYS) | Synchronous dataflow and state machines, qualified code generator | Per a [Berry paper and later material](https://www.academia.edu/88214675/SCADE_Synchronous_Design_and_Validation_of_Embedded_Control_Software), KCG was first released in 1999 and was developed to gradually replace Airbus's internal SAO tool. A [2008 press item](https://www.electronicspecifier.com/design-automation/esterel-technologies-expands-certification-coverage-with-scade) says earlier KCG versions were qualified as a development tool to DO-178B Level A on more than 25 aircraft programs, accepted by EASA, Transport Canada and the FAA, and that KCG 6.0 qualification was to cover the Airbus A400M. Uses cited: fly-by-wire, engine control, brakes, alarms. Also IEC 61508 SIL 3 and EN 50128 SIL 3/4 (TUV SUD certified for rail). Because the generator is qualified, the generated code does not need unit testing. ANSYS acquisition is unsourced. |
| **Simulink + Real-Time Workshop**, later Embedded Coder and Stateflow Coder (MathWorks) | Block diagrams and Stateflow charts to C | Real-Time Workshop was renamed Simulink Coder. Embedded Coder added production-code features and ASAP2 export; AUTOSAR component import/export came with R2008a. Automotive supplier IAV [reported](https://au.mathworks.com/company/user_stories/iav-designs-a-universal-ecu-for-on-target-rapid-prototyping-with-code-generation.html) it avoided hand-coding per microprocessor. |
| **ASCET** (ETAS, a Bosch subsidiary) | Graphical and textual models to ECU code | Reported shipped in over 450 million ECUs ([Infineon page](https://infineon.com/cms/en/tools/aurix-tools/SW-Automation_Autocoding/ETAS)). A [2004 SAE paper, 2004-01-0702](https://www.sae.org/publications/technical-papers/content/2004-01-0702/) compares ASCET-SD, dSPACE TargetLink and Real-Time Workshop/Embedded Coder. |
| **ObjecTime Developer** (ObjecTime Ltd, Kanata, Ontario), then **Rational Rose RealTime** | ROOM modeling to C/C++ | [ROOM book](https://en.wikipedia.org/wiki/ObjecTime) by Selic, Gullekson and Ward, Wiley 1994. Rational collaborated from 1997 and acquired ObjecTime at the start of 2000; the products merged into Rose RealTime. IBM bought Rational in 2002. [Dr. Dobb's 1997 article](https://jacobfilipp.com/DrDobbs/articles/DDJ/1997/9712/9712h/9712h.htm). |
| **IAR visualSTATE** | UML state machine subset to compact C | Per a [2008 feature](https://eejournal.com/article/20080826_model): very compact code for memory-limited parts. IAR also offers [formal verification](https://www.iar.com/visualstate) of the design. Still sold. |
| **Executable UML / BridgePoint** (Project Technology, then Mentor Graphics, now open source) | Shlaer-Mellor method, model compilers for C, C++, VHDL | Method published 1988 and 1991; recast as Executable UML in 2002 ([history paper](https://ceur-ws.org/Vol-1760/paper5.pdf)). BridgePoint editor opened under Apache 2.0 in 2013; One Fact took over maintenance from Mentor ([EXE 2016 slides](https://modelexecution2.big.tuwien.ac.at/wp-content/uploads/exe/exe2016/EXE_2016_slides_paper5.pdf)). Platform-independent and platform-specific models were separated by design, which rules out round-tripping. Kennedy Carter iUML: nothing found in the search, so I cannot confirm details. |
| **Telelogic Tau** (SDL/UML), **TTCN** testing | Telecom-oriented model tools | No review found. Telelogic is described as the top end for embedded work. |

### General-purpose UML and CASE (mostly gone)

| Product | Notes |
|---|---|
| **Rational Rose** | Promised executable code from UML around the time OMG coined Model-Driven Architecture. A [retrospective](https://arxiv.org/pdf/1207.0855) says the effort to keep a model good enough to generate code from often exceeded writing the code. A 2008 dissertation ranked it just behind Together. |
| **Together / TogetherSoft ControlCenter** (then Borland) | A 2003 Japanese [review](https://atmarkit.itmedia.co.jp/fjava/devs/review02/review02_3.html) calls ControlCenter 6.0.1 closer to a development environment than a modeling tool: GUI building, debugging, refactoring, version control. |
| **Artisan Studio** | No review found. |
| **CASE generation (KnowledgeWare IEW, TI IEF, Sterling, Software through Pictures, Teamwork)** | A 1993 GAO report on DoD CASE use found little evidence of quality or productivity benefit. One survey (secondary source) said 73.5% of companies never adopted CASE and 5 of 14 that tried it abandoned it. Sterling bought TI's software division in 1997 ([retrospective](https://developmentcorporate.com/corporate-development/case-tools-vibe-coding-history-repeating/)). Nothing found specific to why any one product failed. |

Also in the same family (unsourced here): LabVIEW, MATRIXx / SystemBuild with Autocode, Esterel Studio, dSPACE TargetLink, Visual Basic-style 4GL generators. Searches for MATRIXx and SystemBuild came back empty.

## Why most of it failed, and the survivors did not

From [Hillel Wayne's piece](https://buttondown.com/hillelwayne/archive/why-uml-really-died/) and the retrospectives found:

- A model detailed enough to generate from is as costly to maintain as the code.
- Generated code was hard to read and change, so developers edited it by hand and the model drifted.
- Tools could generate code from a spec but could not decide what to build.
- UML-as-programming failed early; UML-as-sketching faded slowly.
- The survivors share a pattern: narrow domain, a restricted language with real semantics (synchronous dataflow, statecharts, block diagrams), and a generator that is deterministic and, for avionics, qualified. The code is never touched by hand, so there is no drift.

## The Idea

The old tools lacked the part LLMs are good at: the messy human end. The qualified generators lacked nothing at the back end. So put the LLM at the front, and keep the generator deterministic.

**LLM edits the model, a qualified generator writes the code.** The LLM never emits the final source for the safety-relevant part.

1. **Requirements to model.** The LLM drafts the state machine or dataflow diagram from prose requirements, in the restricted language of an existing qualified tool (SCADE, Simulink/Stateflow, Rhapsody, visualSTATE). Early studies are doing this already: [LLM-generated UML state machines from requirements](https://arxiv.org/html/2604.00275v1) compares GPT-4o and Claude 3.5 Sonnet, and the [lifecycle-aware code generation paper](https://arxiv.org/html/2510.24019v1) found state-machine modeling had the largest effect on generated code quality.
2. **The inline code stays small.** The "write inline code in the action box" step becomes a prompt to the LLM, scoped to one action or guard, with the model as context.
3. **Verify at the model level.** The model is checked by the tool's own formal verification or simulation, plus the LLM generating test scenarios. Verification here is cheaper and stronger than on free-form code, because the language is restricted.
4. **Deterministic, qualified code generation.** The generator emits the code, as before. Certification credit still comes from the generator's qualification, not from trust in the LLM.
5. **Model diff is the review artifact.** Reviewers read a diff of states and transitions, not C. This ties into [ast-mutation-agents-review.md](ast-mutation-agents-review.md): a model edit log is the same structured operation log, and in these tools the tree already exists as the diagram.

Closest existing work, both research-stage:
- [PRISM](https://arxiv.org/html/2510.25890v1): LLM and MDE together, producing machine-checkable evidence for safety-critical domains. Notes most industrial generators still do not emit machine-checkable correctness certificates.
- [Hamburg base.camp hybrid paradigm](https://www.inf.uni-hamburg.de/en/inst/basecamp/projects/archive/2025/48-diederichs-add.html): UML statecharts supply the structure, the LLM fills in the implementation.

## Why this might work now and not before

- The expensive step that killed CASE was writing the detailed model. An LLM can draft it from prose and keep it in sync with changes.
- Drift between model and code is solved the same way the survivors solved it: nobody edits the output.
- The certification argument stays intact. Qualification attaches to the deterministic tool, which is an established route, so there is no need to certify an LLM.

## Risks and open questions

- The LLM can write a wrong model that verifies fine. Verification checks the model against properties, and someone still has to write the properties. This is the old "what should be built" problem.
- Tool qualification covers the generator, not the model. DO-178C or ISO 26262 reviewers will ask how an AI-drafted model was reviewed. No source found shows any regulator accepting AI-in-the-loop modeling.
- The tools are expensive and closed. Open options exist for experiments: BridgePoint xtUML (Apache 2.0), YAKINDU / itemis Create statecharts (appeared in results, details unchecked).
- Most "LLM plus UML" results are 2025-2026 preprints on small examples. No independent industrial evidence found.
- Gains over simply asking an LLM for C may be small for non-safety code. The pitch is strongest where certification or verification is already required.

## Cheap first test

Take 5 small published state-machine requirements (for example from an automotive or avionics standard). Have an LLM produce a model in an open statechart format (SCXML or itemis Create), generate C with the tool, and run the tool's verification. Count how many models verify, and how many of those match a hand-built reference. Compare against asking the LLM for C directly and running the same tests.

## See also

- [ast-mutation-agents-review.md](ast-mutation-agents-review.md): structured edit logs as the diff.
- [agent-work-filing-cabinet.md](agent-work-filing-cabinet.md): provenance of agent outputs.
