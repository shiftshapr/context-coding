# Agent Directory

This directory focuses on the **17 core agents** that cover all essential workflows. Additional specialized agents exist in JAUmemory but these are the primary ones you'll use.

## 17 Core Agents Overview

**Default Workflow Agents** (10 - executed in order):
These agents run automatically in the default workflow: PM → SD → TEST → RED → WHITE → PURPLE → BLINDSPOT → BLUE → DEVOPS → ETHICS

**Specialized Agents** (7 - invoked as needed):
These agents are called when specific expertise is required: ORCH, CR, REFACTOR, DOC, EXP, TS, META

---

## Core Workflow Agents (Default Order - 10 Agents)
| Agent ID | Role | Responsibilities |
| --- | --- | --- |
| `pm` | Project Manager | Problem analysis, requirements validation, create/maintain JAUmemory problem entry, plan diagnostics |
| `sd` | Senior Developer | Solution design, diagnostic script creation, implementation, code walkthrough |
| `test` | Test Engineer | Test strategy, edge cases, diagnostic execution before/after fixes |
| `red` | Red-Line Auditor | Enforce non-negotiable policies, block releases on violations |
| `white` | White-Hat Security | Authentication/authorization review, privacy, secure storage |
| `purple` | Purple-Team Testing | Adversarial testing, attack simulation, failure injection |
| `blindspot` | Blind-Spot Identifier | Surface hidden assumptions, race conditions, integration gaps |
| `blue` | Blue-Hat Final Review | Consolidate findings, ensure all audits pass, update JAUmemory status, final approval |
| `devops` | DevOps Engineer | Deployment planning, CI/CD, monitoring, rollback procedures |
| `ethics` | Ethics & Compliance | Privacy, fairness, governance, accessibility checks |

## Specialized Agents (7 Core - Invoked as Needed)
| Agent ID | Role | Responsibilities |
| --- | --- | --- |
| `orch` | Conductor (Orchestrator) | Initializes workflows, balances workloads, handles 8–10 parallel Orch sessions when tasks can be split |
| `cr` | Code Researcher | Deep debugging, static analysis, runtime tracing |
| `refactor` | Refactor Engineer | Debt reduction, performance optimization, modularization |
| `doc` | Documentation Engineer | Writes/updates docs, tutorials, release notes, JAUmemory summaries |
| `exp` | UX/UI Architect | Interaction design, accessibility, UX guardrails, visual consistency |
| `ts` | TypeScript Specialist | Type safety, migration, type system optimization |
| `meta` | Meta-Learning Agent | Oversees learning process, identifies improvements to how we learn, monitors and intervenes when learning is ineffective, proposes enhancements to JAUmemory usage and pattern detection |

**Note**: These 7 specialized agents are part of the 17 core agents. Use them when you need specific expertise beyond the default workflow.

**META Agent Special Role**:
- **Automatic invocation**: Runs after every learning phase to evaluate its effectiveness
- **Monitoring**: Watches the entire process for learning opportunities and gaps
- **Intervention**: Can be invoked when learning seems ineffective or patterns aren't being captured
- **Improvement proposals**: Suggests enhancements to the learning system itself (JAUmemory structure, pattern detection, agent memory updates, etc.)

## Additional Agents Available in JAUmemory

Beyond the 17 core agents, JAUmemory contains additional specialized agents for specific domains:
- System Debugger variants (`sd1`, `sd2`, `sd3`, `sd4`)
- Test/QA variants (`ta1`, `te1`, `te2`, `qa1`)
- Legacy agents (`pm1`, `de1`, etc.)
- Domain-specific specialists (frontend, backend, integration, etc.)

**To see all available agents**: Query JAUmemory with `list_agents()` to get the complete, real-time roster including UUIDs and personality traits.

## Using Agents Effectively
- **Default workflow** already covers PM→ETHICS; invoke supplemental agents when domain needs extra depth (e.g., `refactor` for performance, `exp` for UX).
- **Parallel orchestration**: ask `orch` to split large tasks into 8–10 subprompts with balanced scope.
- **JAUmemory linking**: whenever an agent produces a major insight, link the memory with `agent_memory({ action: "link", agentId: "sd", memoryId: "mem-123" })`.
- **Reflections**: encourage agents to log `agent_reflection` entries so they improve over time.

This directory will grow as new agents are added. Run `list_agents` via JAUmemory to see the full, real-time roster (including UUIDs and personality traits).
