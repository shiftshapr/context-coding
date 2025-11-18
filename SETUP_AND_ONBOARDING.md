# Setup & Onboarding Guide

Use this playbook to get a new collaborator productive in <30 minutes. Cursor can automate most of it—just paste the commands or ask it to run each step.

## 1. Prerequisites
- **Cursor IDE** (latest build with MCP + JAUmemory access)
- **Node.js 18+** and **npm**
- **Git** (CLI) with GitHub/GitLab access if needed
- **JAUmemory credentials** (ask project owner to invite)
- **Browser with DevTools** (Chrome, Firefox, Edge, etc.)

## 2. Clone the Context Repo
```
git clone <this-repo-url> contextcoding
cd contextcoding
```
> Tip: Ask Cursor, "Clone the contextcoding repo into the workspace and open `TOOLING_OVERVIEW.md`."

## 3. Review Docs in Order
1. `TOOLING_OVERVIEW.md` – overview of every tool
2. `CURSORRULES.md` – red-line policies (must-read)
3. `DEFAULT_WORKFLOW_MANIFEST.md` – workflow & agent order
4. `SYSTEM_PROMPT.md` – copy/paste for orchestration
5. `JAUMEMORY_CONTEXT_QUICKSTART.md` – memory lifecycle
6. `AGENT_DESCRIPTIONS.md` – understand who does what

## 4. Set Up Your Project Repository

### Option A: You Have an Existing Repo
If you're working with an existing project:
```
git clone <your-repo-url> <project-name>
cd <project-name>
npm install  # or yarn install, pnpm install, etc.
npm run lint   # ensure ESLint works
```
> You can tell Cursor: "Set up the project by running npm install and npm run lint" and it will execute the commands.

### Option B: Create a New Repo
If you're starting fresh:

**Say to Cursor**:
```
Help me create a new project repository:
1. Initialize git repo
2. Create package.json with basic structure
3. Set up TypeScript if needed
4. Initialize ESLint configuration
5. Create .gitignore
6. Create initial README.md
```

**Or manually**:
```bash
mkdir my-project
cd my-project
git init
npm init -y
# Add your dependencies and scripts
git add .
git commit -m "Initial commit"
```

## 5. Have Cursor Set Up Project Configuration

**Say to Cursor**:
```
Using the contextcoding directory as reference:
1. Read CURSORRULES.md and create a .cursorrules file in this project root
2. Read DEFAULT_WORKFLOW_MANIFEST.md and store the workflow definition in JAUmemory
3. Read AGENT_DESCRIPTIONS.md and ensure all agents are available/configured in JAUmemory
4. Set up any project-specific guardrails based on the templates
```

**Cursor will**:
- Create `.cursorrules` file in your project root
- Store workflow manifest in JAUmemory for recall
- Verify agents are available
- Configure project-specific policies

## 6. Connect to JAUmemory
1. Open Cursor command palette → `JAUmemory: Authenticate`
2. Provide credentials when prompted
3. Test with: "Recall any memories about [your-project-name]"
4. Create a collection for your work stream if needed

**Say to Cursor**:
```
Test JAUmemory by listing all available agents and creating a test memory for project [your-project-name]
```

## 7. Set Up Text Replacement for System Prompt (Recommended)

**Why**: The system prompt is long and you'll use it frequently. Set up a text expansion shortcut.

**Tools** (choose one):
- **macOS**: TextExpander, aText, or built-in Text Replacement (System Settings → Keyboard → Text Replacements)
- **Windows**: PhraseExpress, TextExpander, or AutoHotkey
- **Linux**: AutoKey, Espanso, or TextExpander

**Setup**:
1. Open your text replacement tool
2. Create a new snippet/expansion
3. **Shortcut**: `;orch` or `;system` (or your preference)
4. **Expansion**: Copy the entire contents of `SYSTEM_PROMPT.md`
5. **Placeholder**: Replace `[describe bug clearly]` with `{{bug}}` or `%bug%` (if your tool supports placeholders)

**Usage**:
- Type `;orch` anywhere in Cursor chat
- It expands to the full system prompt
- Replace `[describe bug clearly]` with your actual task description
- Add browser console logs if relevant (see Browser Console section)
- Send to Cursor

**Alternative**: If your tool doesn't support placeholders, just use `;orch` and manually replace `[describe bug clearly]` each time.

## 8. Browser Console Tool

**Purpose**: Capture runtime errors, network requests, state snapshots, and diagnostic data from your web application.

**How to Use**:
1. Open your web app in browser
2. Open DevTools (F12 or Cmd+Option+I / Ctrl+Shift+I)
3. Go to **Console** tab
4. When reporting bugs, include:
   - **Errors**: Red error messages with stack traces
   - **Warnings**: Yellow warning messages
   - **Network requests**: Go to Network tab, filter by XHR/Fetch, copy failed requests
   - **State snapshots**: Run diagnostic commands, copy output
   - **LocalStorage/SessionStorage**: Check Application/Storage tab for relevant data

**Say to Cursor when reporting bugs**:
```
Fix [describe bug]. Here are the browser console logs:
[Paste console errors, warnings, network failures, and any diagnostic output]
```

**Pro Tips**:
- Use `console.table()` to format object arrays nicely
- Use `console.group()` to organize related logs
- Filter console by "Errors" to see only critical issues
- Export console logs: Right-click console → "Save as..."
- Use Network tab to see failed API calls with request/response details

**Example Console Output to Include**:
```
Error: Cannot read property 'theme' of undefined
    at UserPreferencesManager.getPreference (UserPreferencesManager.js:45)
    at ProfileManager.toggleTheme (ProfileManager.js:123)

Network Request Failed:
GET /api/v1/users/123 500 Internal Server Error
Response: {"error": "Database connection failed"}
```

## 9. Using the System Prompt
1. Type your shortcut (e.g., `;orch`) or copy from `SYSTEM_PROMPT.md`
2. Replace `[describe bug clearly]` with your task
3. **Add browser console logs** if the issue involves runtime errors, network failures, or state issues
4. Replace `Active project = [project-name]` with your actual project name
5. Paste into Cursor chat
6. Approve diagnostic script creation when prompted
7. If Cursor asks whether to spin up 8–10 Orch sessions (for large refactors), answer yes/no and let it generate the sub-prompts

## 10. Ask Cursor for Help Automating Setup
Sample prompts:
- "Cursor, read `contextcoding/TOOLING_OVERVIEW.md` and summarize the workflow."
- "Cursor, create JAUmemory entries for the problems we find today."
- "Cursor, split this refactor across 10 Orch tasks with balanced effort."
- "Cursor, check the distribution for stray markdown files and archive them."
- "Cursor, set up .cursorrules based on the template in contextcoding/CURSORRULES.md"

## 11. Optional: Create Additional Workflows
If your team needs a custom workflow:

**Say to Cursor**:
```
Create a custom workflow based on DEFAULT_WORKFLOW_MANIFEST.md:
- Modify agent order to: [your-order]
- Add/remove agents: [list changes]
- Save as workflows/[workflow-name].md
- Store in JAUmemory for future recall
```

## 12. Verification Checklist
- [ ] Cursor installed & authenticated
- [ ] Context repo cloned
- [ ] Project repo set up (existing or new)
- [ ] `.cursorrules` created in project root
- [ ] Workflow stored in JAUmemory
- [ ] Agents verified in JAUmemory
- [ ] JAUmemory access verified
- [ ] Text replacement shortcut configured (`;orch`)
- [ ] Browser DevTools accessible
- [ ] System prompt tested on a sample task
- [ ] Understanding of guardrails confirmed

Once these boxes are checked, the collaborator is ready to ship.
