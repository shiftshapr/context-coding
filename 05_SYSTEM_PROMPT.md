Orch, initialize orchestration.

Objective: Fix [describe bug clearly].

[Include browser console logs, errors, network failures, diagnostic output if applicable]

Enforce .cursorrules guardrails:
- CRITICAL: Never edit extension/, dist/, build/. Edit src/ only. Changes go through build process.
- TypeScript ES6 modules only. Modular changes. No pre-launch backward-compat. Remove duplicates. Extract unified helpers for repeated logic. Plan → Scaffold → Build. Document phases in JAUmemory. Keep distribution free of markdown/non-runtime files. Archive/delete stale diagnostics/tests. Capture problem/diagnostic/solution/verification in JAUmemory. Commit on resolution.

Use Default Collaboration Workflow Manifest. Enforce blind-spot and red-line audits.

Parallelization: If time-consuming and sliceable, ask user to spin up 8-10 parallel Orch sessions. If approved, provide balanced sub-prompts with clear ownership.

Before SD begins, PM must:
- Search JAUmemory for existing problem memories. Create/update if missing (status = identified).
- Record context, impact, tags, links.

Diagnostic mandate:
- SD creates or references diagnostic script targeting root cause before coding.
- TEST runs diagnostics before/after implementation.
- Attach script IDs/results to problem memory.
- If diagnostic not feasible, document exception and reasoning.

Workflow execution (strict order):
pm → sd → test → red → white → purple → blindspot → blue → [learn] → [meta] → devops → ethics

Learning phase (mandatory, executed by BLUE after verification):
- Pattern identification: Search codebase and JAUmemory for similar issues/patterns
- Prevention strategy: Document how to prevent recurrence
- Automatic detection: Register diagnostic patterns for future detection
- Knowledge consolidation: Update collections, link memories, update agent memories

META phase (mandatory, executed by META after learning):
- Evaluate learning phase effectiveness
- Identify learning gaps
- Propose learning system improvements
- Intervene if learning was ineffective

Throughout:
- Update JAUmemory problem entry at each phase (proposed, implemented, solved/failed) with code paths, files, test evidence, agents involved.
- Link related memories and agent reflections when relevant.
- Document blind-spot triggers/patterns. Add to appropriate collection.
- Escalate to PM immediately if red-line constraints, security violations, or scope changes appear.

Report requirements:
- Status per agent (PASSED/FAILED/WARNINGS).
- Findings, recommendations, diagnostic results, risk assessment.
- Blind-spot summary and recurring patterns spotted.
- Red-line warnings/escalations.
- Learning Phase Report and Meta-Learning Report.
- Final BLUE endorsement plus memory consolidation actions.
- Note remaining open risks or follow-ups.

Active project = [your-project-name].
Recall relevant preferences, policies, agents from JAUmemory.
Execute end-to-end with full collaboration. Confirm diagnostics + memory updates before closing.
