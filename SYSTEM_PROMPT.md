Orch, initialize orchestration using the Task Invocation Template.

Objective:
Fix [describe bug clearly].

Apply `.cursorrules` guardrails at every step:
- TypeScript + ES6 modules only, modularized changes
- No pre-launch backward-compat paths or fallbacks; remove duplicates instead
- Always look for repeated logic and extract unified helpers/modules, noting decisions in JAUmemory
- Plan → Scaffold → Build, documenting each phase in JAUmemory
- Keep extension distribution free of markdown/non-runtime files; archive or delete stale diagnostics/tests
- Always capture problem/diagnostic/solution/verification details in JAUmemory and commit on resolution

Use the Default Collaboration Workflow Manifest and enforce all blind-spot and red-line audits.

Parallelization policy:
If this task is time-consuming but sliceable (e.g., medium refactor/cleanup), ask the user whether to spin up 8–10 parallel Orch sessions and, if approved, provide balanced sub-prompts with clear ownership.

Before SD begins, PM must search JAUmemory for existing problem memories, create/update one if missing (status = identified), and note diagnostic requirements.

Diagnostic mandate:
- SD creates or references a diagnostic script targeting the root cause before coding
- TEST runs diagnostics before and after implementation
- Attach script IDs/results + verification output to the problem memory; document any exception

Active project = canopi. Recall all relevant preferences, policies, and agents from JAUmemory.

Execute the task end-to-end with full agent collaboration:
pm → sd → test → red → white → purple → blindspot → blue → devops → ethics.

Report results including:
- Status per agent (PASSED/FAILED/WARNINGS) with findings/recommendations/risks
- Diagnostic results and blind-spot patterns (link to collections)
- Red-line warnings or escalations
- Final BLUE confirmation, commit reference, and JAUmemory status updates
