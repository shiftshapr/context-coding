# AI Coding Tools Overview

This guide explains all the tools available for AI-assisted coding in this project.

## Core Orchestration Tools

### 1. System Prompt
**Location**: `05_SYSTEM_PROMPT.md`

The system prompt is your primary orchestration command. It:
- Initializes the full 10-agent collaboration workflow
- Enforces `.cursorrules` guardrails automatically
- Triggers JAUmemory problem tracking
- Requires diagnostic scripts for root cause analysis
- Can parallelize large tasks across 8-10 Orch sessions

**Usage**: Copy the prompt from `05_SYSTEM_PROMPT.md`, replace `[describe bug clearly]` with your task, and send it to Cursor.

**Pro Tip: Text Replacement Shortcut**
Set up a text expansion tool (TextExpander, aText, AutoKey, etc.) with shortcut `;orch` that expands to the full system prompt. This saves time since you'll use it frequently.

**Setup**:
1. Install a text replacement tool (macOS: TextExpander/aText, Windows: PhraseExpress/AutoHotkey, Linux: AutoKey/Espanso)
2. Create snippet with shortcut `;orch` (or your preference)
3. Copy entire `05_SYSTEM_PROMPT.md` content as expansion
4. Type `;orch` anywhere → expands to full prompt → replace `[describe bug clearly]` → send

**Key Features**:
- Automatic JAUmemory problem cataloging
- Diagnostic script mandate
- Parallel orchestration for time-consuming tasks
- Full agent audit chain (pm → sd → test → red → white → purple → blindspot → blue → devops → ethics)

### 2. Cursor Rules (`.cursorrules`)
**Location**: 
- `07a_CURSORRULES_GENERIC.md` – Universal rules for all projects
- `07b_CURSORRULES_EXTENSION_EXAMPLE.md` – Extension-specific rules (only if building browser extensions)
- `06_CURSORRULES.md` – Index file explaining which to use

Red-line policies that are **automatically enforced** by all agents:

**Field Naming**:
- ✅ Use camelCase everywhere (`createdAt`, `userId`, `pageId`)
- ❌ NO snake_case (`created_at`, `user_id`)
- ❌ NO duplicate fields with different naming
- Convert at interface boundaries, delete originals

**Extension Distribution Cleanliness** (Extension projects only - see `07b_CURSORRULES_EXTENSION_EXAMPLE.md`):
- ❌ NO `.md` files in distribution directory
- ❌ NO TypeScript source files in distribution
- ❌ NO test files, build scripts, or diagnostic scripts in distribution
- ✅ All documentation goes in `docs/` or parent directory
- ✅ Archive or delete stale files; move to `archive/` if needed

**Code Quality**:
- ✅ TypeScript + ES6 modules only
- ✅ Modular architecture
- ✅ Always create unified functions for repeated code
- ✅ No backward compatibility pre-launch
- ✅ Check for duplication before adding new code
- ✅ Plan → Scaffold → Build process
- ✅ Always log to JAUmemory
- ✅ Avoid fallbacks
- ✅ Commit on resolution

**TypeScript Safety**:
- Null checks for DOM access
- Event handler cleanup
- Async error handling
- Window global null checks
- Type guards instead of `any`

### 3. Agents (16 Core Agents)
**Location**: JAUmemory (query with `list_agents`)

The system has **16 core agents** that cover all essential workflows. Additional specialized agents are available but these are the primary ones:

**Default Workflow Agents** (10 - executed in order):
- `pm` (Project Manager) - Problem analysis, JAUmemory tracking, diagnostic planning
- `sd` (Senior Developer) - Solution design, implementation, diagnostic scripts
- `test` (Test Engineer) - Test strategy, verification, diagnostic execution
- `red` (Red-Line Auditor) - Policy enforcement, blocks violations
- `white` (White-Hat Security) - Security review, authentication, privacy
- `purple` (Purple-Team Testing) - Adversarial testing, attack simulation
- `blindspot` (Blind-Spot Identifier) - Edge cases, race conditions, hidden assumptions
- `blue` (Blue-Hat Final Review) - Final approval, JAUmemory status updates
- `devops` (DevOps Engineer) - Deployment, CI/CD, monitoring
- `ethics` (Ethics & Compliance) - Privacy, fairness, governance

**Specialized Agents** (6 - invoked as needed):
- `orch` (Conductor) - Orchestrates workflows, handles parallelization (8-10 Orch sessions)
- `cr` (Code Researcher) - Deep debugging, static analysis, runtime tracing
- `refactor` (Refactor Engineer) - Code optimization, debt reduction, performance
- `doc` (Documentation Engineer) - Technical writing, tutorials, knowledge transfer
- `exp` (UX/UI Architect) - User experience, accessibility, interaction design
- `ts` (TypeScript Specialist) - Type safety, migration, type system optimization

**Note**: Additional specialized agents exist in JAUmemory for specific domains. Query `list_agents()` to see all available agents.

**Usage**: Agents are automatically invoked in the workflow. You can also:
- Query agent memories: `agent_memory({ action: "recall", agentId: "sd" })`
- Link problems to agents: `agent_memory({ action: "link", agentId: "sd", memoryId: "..." })`
- Get agent reflections: `agent_reflection({ action: "list", agentId: "sd" })`

### 4. JAUmemory System

#### Memories
**Purpose**: Track problems, solutions, learnings, and patterns

**Key Operations**:
- `remember()` - Store new memory (problem, solution, learning)
- `recall()` - Search memories by query/tags
- `update()` - Update existing memory
- `forget()` - Delete memory
- `analyze()` - Analyze memory patterns over time
- `consolidate()` - Group similar memories into insights

**Memory Lifecycle** (for problems):
1. `identified` - Problem discovered
2. `proposed` - Solution designed
3. `implemented` - Code written
4. `solved` / `failed` - Verification complete

**Best Practices**:
- Always search before creating (avoid duplicates)
- Use consistent tags (e.g., "bug", "frontend", "database")
- Link related memories
- Update status throughout workflow
- Include context, impact, affected files

#### Collections
**Purpose**: Organize related memories by theme

**Operations**:
- `create_collection()` - Create new collection
- `add_to_collection()` - Add memory to collection
- `get_collection()` - View all memories in collection
- `consolidate_collection()` - Create summary from collection
- `list_collections()` - See all collections

**Example Collections**:
- "Blind-Spot Radar" - Recurring edge cases
- "Realtime Sync Issues" - Related problems
- "Diagnostic Library" - Diagnostic scripts
- "Theme-related Problems" - UI/UX issues

#### Agent Memories
**Purpose**: Link memories to specific agents for learning

**Operations**:
- `agent_memory({ action: "link" })` - Link memory to agent
- `agent_memory({ action: "recall" })` - Get agent's memories
- `agent_error_learning()` - Track agent errors and solutions
- `agent_reflection()` - Store agent learnings

### 5. Default Workflow
**Location**: `08_DEFAULT_WORKFLOW_MANIFEST.md`

**Execution Order**:
```
PM → SD → TEST → RED → WHITE → PURPLE → BLINDSPOT → BLUE → DEVOPS → ETHICS
```

**Each Agent Must**:
1. Check JAUmemory for existing problems
2. Create/update problem memory if needed
3. Create diagnostic scripts (SD)
4. Execute diagnostics (TEST)
5. Produce status report (PASSED/FAILED/WARNINGS)
6. Update JAUmemory with findings
7. Link to related memories/agents

**Reporting Requirements**:
- Status per agent
- Findings and recommendations
- Risk assessment
- Diagnostic results
- Blind-spot analysis
- Red-line audit results
- Final BLUE approval

### 6. Custom Workflows
**Ability**: Create additional workflows beyond the default

**How to Set Up**:
1. Define workflow in JAUmemory as a memory or collection
2. Specify agent order and responsibilities
3. Create workflow manifest document (similar to `08_DEFAULT_WORKFLOW_MANIFEST.md`)
4. Reference in system prompt: "Use Custom Workflow X instead of default"

**Example Use Cases**:
- Quick bug fix workflow (pm → sd → test → blue)
- Security audit workflow (red → white → purple → blue)
- Documentation workflow (doc → pm → blue)
- Refactoring workflow (refactor → sd → test → blue)

## Development Tools

### 7. Cursor IDE
**Features Available**:
- **Multi-agent orchestration** - Automatic agent collaboration
- **Inline AI commands** - `/fix`, `/explain`, `/refactor`
- **Terminal integration** - Run commands directly
- **File tree navigation** - Quick file access
- **Diff viewer** - See changes before committing
- **Lint integration** - Real-time error detection
- **Git integration** - Commit, push, branch management
- **MCP tools** - JAUmemory, diagnostics, todos

**Usage Tips**:
- Use Cmd/Ctrl+K for inline edits
- Use Cmd/Ctrl+L for chat
- Right-click files for context menu
- Use terminal for npm/git commands

### 8. Browser Console (DevTools)
**Purpose**: Capture runtime errors, network requests, state snapshots, and diagnostic data

**How to Access**:
- **Chrome/Edge**: F12 or Cmd+Option+I (Mac) / Ctrl+Shift+I (Windows/Linux)
- **Firefox**: F12 or Cmd+Option+K (Mac) / Ctrl+Shift+K (Windows/Linux)
- **Safari**: Cmd+Option+C (enable Developer menu first)

**Key Tabs**:
- **Console**: Errors, warnings, logged output, interactive JavaScript execution
- **Network**: All HTTP requests, response times, failed requests, request/response payloads
- **Application/Storage**: LocalStorage, SessionStorage, IndexedDB, Cookies
- **Elements**: DOM inspection, computed styles, event listeners

**When Reporting Bugs**:
1. Open Console tab, filter by "Errors"
2. Copy all red error messages with stack traces
3. Check Network tab for failed requests (status 4xx/5xx)
4. Include request URL, method, headers, and response body
5. If state-related, run diagnostic commands and copy output

**Say to Cursor**:
```
Fix [describe bug]. Browser console shows:
[Paste errors, warnings, network failures, diagnostic output]
```

**Pro Tips**:
- Use `console.table(array)` to format object arrays
- Use `console.group()` to organize related logs
- Export console: Right-click → "Save as..."
- Use Network tab filters (XHR, Fetch, WS) to find API calls
- Check "Preserve log" to keep logs across page reloads

**Example Output to Include**:
```
Console Error:
Error: Cannot read property 'theme' of undefined
    at UserPreferencesManager.getPreference (UserPreferencesManager.js:45)
    at ProfileManager.toggleTheme (ProfileManager.js:123)

Network Failure:
GET /api/v1/users/123 → 500 Internal Server Error
Request Headers: { Authorization: "Bearer ..." }
Response: {"error": "Database connection failed"}
```

### 9. Git & Rollbacks
**Available Commands**:
- `git status` - Check current state
- `git diff` - See changes
- `git log` - View history
- `git revert <commit>` - Undo specific commit
- `git reset --hard <commit>` - Reset to specific commit
- `git restore <file>` - Restore specific file
- `git checkout <branch>` - Switch branches

**Cursor AI Undo**:
- Cursor tracks AI-generated edits
- Can undo AI changes separately from manual edits
- Still use git for full history control

**Best Practice**:
- Commit after each resolved problem (per guardrails)
- Include JAUmemory problem ID in commit message
- Use branches for experimental changes

### 10. ESLint Setup
**Location**: Repo root (`.eslintrc`, `package.json`)

**Included in Repo**:
- ✅ ESLint configuration file
- ✅ TypeScript rules
- ✅ Custom project rules
- ✅ Lint scripts in `package.json`

**Setup** (after cloning):
```bash
npm install  # Installs ESLint and dependencies
npm run lint  # Run linting
```

**Cursor Integration**:
- Real-time lint errors in IDE
- Red squiggles for violations
- Auto-fix available for many rules
- `read_lints` tool for programmatic access

**Key Rules Enforced**:
- TypeScript strict mode
- No `any` types (use `unknown` + guards)
- ES6 modules only
- Proper null checks
- Event handler cleanup
- Async error handling

## Workflow Integration

### How Tools Work Together

1. **Start Task**: Use system prompt → triggers workflow
2. **Enforcement**: `.cursorrules` automatically applied
3. **Tracking**: JAUmemory stores problem/solution lifecycle
4. **Diagnostics**: Diagnostic scripts created and executed
5. **Quality**: ESLint catches issues, agents audit
6. **Completion**: BLUE approves, commit made, JAUmemory updated

### Quick Reference

**For a new bug fix**:
1. Copy `05_SYSTEM_PROMPT.md`
2. Replace objective with bug description
3. Send to Cursor
4. Agents automatically:
   - Check JAUmemory
   - Create diagnostic
   - Fix code
   - Run tests
   - Audit compliance
   - Update memory
   - Request commit

**For a large refactor**:
1. Use system prompt
2. When prompted, approve parallel orchestration
3. Receive 8-10 balanced sub-prompts
4. Execute in parallel Orch sessions
5. Merge results

**For learning from past work**:
1. Query JAUmemory: `recall({ query: "theme saving" })`
2. Review related memories
3. Check agent memories: `agent_memory({ action: "recall", agentId: "sd" })`
4. View collections: `get_collection({ collection_id: "..." })`

## Getting Started Checklist

- [ ] Clone repo and run `npm install`
- [ ] Review `07a_CURSORRULES_GENERIC.md` for red-line policies
- [ ] Review `08_DEFAULT_WORKFLOW_MANIFEST.md` for workflow
- [ ] Review `09_JAUMEMORY_CONTEXT_QUICKSTART.md` for memory practices
- [ ] Test system prompt with a small task
- [ ] Verify ESLint is working (`npm run lint`)
- [ ] Set up JAUmemory access (if needed)
- [ ] Review available agents (`list_agents`)

## Support

- **Workflow questions**: See `08_DEFAULT_WORKFLOW_MANIFEST.md`
- **Policy questions**: See `07a_CURSORRULES_GENERIC.md` (and `07b_CURSORRULES_EXTENSION_EXAMPLE.md` if building extensions)
- **Memory questions**: See `09_JAUMEMORY_CONTEXT_QUICKSTART.md`
- **Agent questions**: Query JAUmemory `list_agents()`

