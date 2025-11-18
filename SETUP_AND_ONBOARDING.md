# Setup & Onboarding Guide

Use this playbook to get a new collaborator productive in <30 minutes. Cursor can automate most of it—just paste the commands or ask it to run each step.

## 1. Prerequisites
- **Cursor IDE** (latest build with MCP + JAUmemory access)
- **Node.js 18+** and **npm**
- **Git** (CLI) with GitHub/GitLab access if needed
- **JAUmemory credentials** (ask project owner to invite)

## 2. Clone the Context Repo
```
git clone <this-repo-url> contextcoding
cd contextcoding
```
> Tip: Ask Cursor, “Clone the contextcoding repo into the workspace and open `docs/TOOLING_OVERVIEW.md`.”

## 3. Review Docs in Order
1. `docs/TOOLING_OVERVIEW.md` – overview of every tool
2. `docs/CURSORRULES.md` – red-line policies (must-read)
3. `docs/DEFAULT_WORKFLOW_MANIFEST.md` – workflow & agent order
4. `docs/SYSTEM_PROMPT.md` – copy/paste for orchestration
5. `docs/JAUMEMORY_CONTEXT_QUICKSTART.md` – memory lifecycle
6. `docs/AGENT_DESCRIPTIONS.md` – understand who does what

## 4. Configure Local Environment
If you’re also working in the main product repo (e.g., `metalayer-initiative`):
```
git clone <product-repo-url>
cd metalayer-initiative
npm install
npm run lint   # ensure ESLint works
```
> You can tell Cursor: “Set up the project by running npm install and npm run lint” and it will execute the commands.

## 5. Connect to JAUmemory
1. Open Cursor command palette → `JAUmemory: Authenticate`
2. Provide credentials when prompted
3. Test with `recall({ query: "preferences" })`
4. Create a collection for your work stream if needed

## 6. Using the System Prompt
1. Copy `docs/SYSTEM_PROMPT.md`
2. Replace `[describe bug clearly]` with your task
3. Paste into Cursor chat
4. Approve diagnostic script creation when prompted
5. If Cursor asks whether to spin up 8–10 Orch sessions (for large refactors), answer yes/no and let it generate the sub-prompts

## 7. Workflow Reminders
- Always execute `pm → sd → test → red → white → purple → blindspot → blue → devops → ethics`
- Every phase must update the JAUmemory problem entry (status + findings)
- Diagnostic scripts are mandatory unless explicitly documented as infeasible
- Remove markdown/non-runtime files from extension distribution; archive unused assets
- Commit after BLUE approval and reference the JAUmemory ID in the message

## 8. Ask Cursor for Help Automating Setup
Sample prompts:
- “Cursor, read `contextcoding/docs/TOOLING_OVERVIEW.md` and summarize the workflow.”
- “Cursor, create JAUmemory entries for the problems we find today.”
- “Cursor, split this refactor across 10 Orch tasks with balanced effort.”
- “Cursor, check the distribution for stray markdown files and archive them.”

## 9. Optional: Create Additional Workflows
If your team needs a custom workflow:
1. Duplicate `docs/DEFAULT_WORKFLOW_MANIFEST.md`
2. Modify agent order/responsibilities
3. Save as `docs/workflows/<name>.md`
4. Update the system prompt to reference the new workflow

## 10. Verification Checklist
- [ ] Cursor installed & authenticated
- [ ] Context repo cloned
- [ ] Product repo cloned & lint passes
- [ ] JAUmemory access verified
- [ ] System prompt tested on a sample task
- [ ] Understanding of guardrails confirmed

Once these boxes are checked, the collaborator is ready to ship.
