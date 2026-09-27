# Agent Sandbox as a Service

## Problem

Running AI coding agents (Claude Code, Cursor, custom agents) against a real enterprise codebase is harder than it looks. A developer laptop can't sustain long-running or parallel agent sessions. Sharing credentials, clones, secrets, and tool access across a team multiplies the setup burden per person. When Alexey runs agents in Docker containers locally, he's solving the same coordination problem that remote VSCode sessions on EC2 solved for interactive development. The friction is the same; only the workload changed.

Gitpod (valued at $400M before its 2025 rebrand and acquisition by OpenAI as "Ona") and GitHub Codespaces proved that this "small" problem - provisioning and sharing dev environments - is a viable enterprise business at scale. The same opportunity is opening up again, now for agentic workloads.

## The Idea

A platform that provisions isolated, pre-configured cloud environments ("sandboxes") for AI agents on demand - analogous to what Gitpod/Codespaces did for human developers. Each sandbox gets:

- a clone of the codebase
- pre-installed toolchains (Docker, kubectl, Python, Node, Claude Code CLI, etc.)
- injected secrets (API tokens, ECR access, SSM) without developer exposure
- isolation between tenants (per-agent or per-user)
- fast boot and teardown
- optionally: persistent state between sessions (snapshot/resume)

Concretely: Alexey clicks "run agent on PR #412," the platform spins up a sandbox, the agent works, the result is a commit or test run. No local Docker setup, no credential sharing in Slack.

## Connection to qSpark Work

DVN-1606 (Done) was a step in this direction: an AWX template to spin up a shared t3.medium EC2 for Claude Code remote sessions with per-user home directories, pre-installed tooling, and secrets injection. That is the lowest rung of the ladder. A scalable version would add on-demand provisioning, multi-agent parallelism, and tighter codebase/secret integration.

## Market Landscape (as of 2025-2026)

The space has matured rapidly after the OpenAI Agents SDK (April 2026) made sandboxes a first-class primitive with seven built-in providers.

**Open source / self-hostable:**
- [E2B](https://e2b.dev) - Apache-2.0, Firecracker microVM isolation, purpose-built for AI agents, ~$0.05/hr per 1 vCPU sandbox. Actively maintained.
- [Coder](https://coder.com) - AGPLv3, workspace-per-developer model, strong self-hosting story.
- [SkyPilot](https://github.com/skypilot-org/skypilot) - orchestrates LLM sandboxes on your own cloud (EC2, GCP, etc.) in ~10 minutes.

**Commercial (closed or partially open):**
- [Daytona](https://daytona.io) - pivoted to agent infra Feb 2025, raised $24M Series A (Feb 2026), sub-90ms sandbox boot, stateful/snapshotted. Went closed-source June 2026.
- [Modal](https://modal.com) - container-based, pay-per-second, strong Python ecosystem.
- [Blaxel](https://blaxel.ai) - microVM isolation, includes MCP server hosting and model gateway.
- [Runloop](https://runloop.ai), [Northflank](https://northflank.com) - similar positioning.
- GitHub Codespaces / Gitpod (now Ona, acquired by OpenAI Jun 2026) - human-developer-centric; Ona pivoting to AI engineering.

**Curated list:** [awesome-sandbox](https://github.com/restyler/awesome-sandbox)

## Business Angle

The Gitpod story is instructive: a problem that sounds like DevOps housekeeping turned into a $400M valuation because every mid-size engineering team eventually hits it. Agent sandboxing is at the same inflection point. Daytona reached $1M ARR in under three months after pivoting. E2B is used by ~half the Fortune 500 for AI agent infrastructure.

A defensible niche: enterprise self-hosted, with deep integration into internal tooling (Ansible/AWX provisioning, Consul service discovery, Vault/SSM secrets, per-cluster Kubernetes targets) - the gap the big SaaS players don't serve well.

## Links

- [E2B vs Daytona comparison (Northflank)](https://northflank.com/blog/daytona-vs-e2b-ai-code-execution-sandboxes)
- [Best cloud sandboxes for AI agents 2026 (Blaxel)](https://blaxel.ai/blog/best-cloud-sandboxes-ai-agents-2026)
- [Ephemeral dev environments for coding agents (Qovery)](https://www.qovery.com/blog/ephemeral-dev-environments-for-coding-agents-platforms-compared)
- [E2B vs Daytona vs Modal self-host comparison](https://bex.co/blog/2026/09/14/ai-agent-sandbox-market-e2b-modal-daytona)
- [SkyPilot self-hosted LLM sandbox](https://blog.skypilot.co/skypilot-llm-sandbox/)
- [DVN-1606 - qSpark shared EC2 for Claude Code](https://qspark.atlassian.net/browse/DVN-1606)
