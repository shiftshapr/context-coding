# JAUmemory Context Quickstart

This is the minimum context we share with collaborators so they can plug into the orchestration workflow immediately.

## 1. Problem & Solution Lifecycle
- Always search JAUmemory before creating anything new (keywords + tags + project = canopi).
- If no match, create a problem memory with: content, context, impact, affected files/systems, severity, owner, and status `identified`.
- Update the same memory as work progresses: `proposed` (solution plan), `implemented` (code details + files), `solved/failed` (verification + lessons).
- Link related memories (prior incidents, diagnostics, agent reflections) so patterns surface automatically.

## 2. Diagnostic Script Requirement
- Every task needs a diagnostic script dedicated to the root cause you are chasing (unless explicitly documented as infeasible/time-critical).
- Use `/presence/utils/ROOT_CAUSE_DIAGNOSTIC_FRAMEWORK.js` as the scaffold; register a named diagnostic and capture output.
- Store diagnostic IDs, inputs, and results inside the associated JAUmemory entry so future runs can replay them.

## 3. Blind-Spot Intelligence
- BLINDSPOT agent outputs must be recorded as their own memories (edge-case description, trigger conditions, mitigations, owners).
- Tag these with `blindspot` + component tags and add them to the "Blind-Spot Radar" collection so we can query recurring triggers.
- When similar issues appear, link the new problem to prior blind-spot memories before coding.

## 4. Reporting & Escalation
- Each agent status update (PASSED/FAILED/WARNINGS) must be logged back into the problem memory along with findings, recommendations, risk level, and diagnostic evidence.
- Escalate to PM immediately when a red-line, security violation, or scope change appears—note the escalation record in JAUmemory.

## 5. Collections & Consolidation
- Use collections for theme-based tracking (e.g., `realtime-sync`, `presence-ui`, `diagnostic-library`).
- After BLUE approval, consolidate related memories into insights monthly so we get summarized lessons.
- Link solved problems to participating agents using agent memories so we can query "what did SD learn last month?" quickly.

Keeping these habits ensures the knowledge graph stays fresh and everyone can ramp fast.
