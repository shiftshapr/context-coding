# Agent Directory

This is the canonical list of agents currently available in JAUmemory-based orchestration. Use it to select the right specialist when customizing workflows.

## Core Workflow Agents (Default Order)
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

## Orchestration & Strategy
| Agent ID | Role | Responsibilities |
| --- | --- | --- |
| `orch` | Conductor (Orchestrator) | Initializes workflows, balances workloads, handles 8–10 parallel Orch sessions when tasks can be split |
| `prod` | Product Strategist | Aligns work with user outcomes, metrics, and roadmap |
| `doc` | Documentation Engineer | Writes/updates docs, tutorials, release notes, JAUmemory summaries |
| `exp` | UX/UI Architect | Interaction design, accessibility, UX guardrails, visual consistency |
| `refactor` | Refactor Engineer | Debt reduction, performance optimization, modularization |
| `int` | Integration Engineer | API schemas, data pipelines, cross-service glue |
| `blindspot` | Blind-Spot Analyst | Already listed above; double-emphasized due to importance |

## Security Suite
| Agent ID | Role | Notes |
| --- | --- | --- |
| `red` | Critical constraint auditor | Stops work on policy breaches |
| `white` | Security integrity | Threat modeling, auth flows |
| `purple` | Adversarial tester | Attack simulations, fuzzing |
| `blue` | Final QA/security gate | Signs off only when all others pass |

## Diagnostics & Research
| Agent ID | Role | Responsibilities |
| --- | --- | --- |
| `cr` | Code Researcher | Deep debugging, static analysis, runtime tracing |
| `sd1`/`sd2`/`sd3`/`sd4` | System Debugger variants | Focus areas: architecture-first, cleanup, COMP compliance, frontend debugging |
| `ta1`, `te1`, `te2`, `qa1` | Test/QA variants | Automation, chrome extensions, diagnostics, manual QA |
| `blindspot` | Already above | – |

## Additional Specialized Agents
| Agent ID | Role | Responsibilities |
| --- | --- | --- |
| `devops` (legacy `de1`) | Ops engineer | Infrastructure, monitoring, security hardening |
| `pm1` | Legacy PM | Older workflows; kept for compatibility |
| `doc` | Documentation | Tutorials, knowledge transfer |
| `code-reviewer` | Reviewer | Detailed code review focus |
| `syntax fixer (sxf1)` | Syntax Fixer | Fast syntax cleanup |
| `senior frontend developer` | Frontend specialist | CSS/UX enhancements |
| `cross-profile sync specialist (cp1)` | Realtime sync | Multi-profile broadcast issues |

## Using Agents Effectively
- **Default workflow** already covers PM→ETHICS; invoke supplemental agents when domain needs extra depth (e.g., `refactor` for performance, `exp` for UX).
- **Parallel orchestration**: ask `orch` to split large tasks into 8–10 subprompts with balanced scope.
- **JAUmemory linking**: whenever an agent produces a major insight, link the memory with `agent_memory({ action: "link", agentId: "sd", memoryId: "mem-123" })`.
- **Reflections**: encourage agents to log `agent_reflection` entries so they improve over time.

This directory will grow as new agents are added. Run `list_agents` via JAUmemory to see the full, real-time roster (including UUIDs and personality traits).
