# Complete Workflow Guide

This guide walks you through the complete process of working with the orchestration system from task identification to completion.

## Overview

The workflow follows this pattern:
1. **Plan** (with PM) → 2. **Review & Refine** → 3. **Execute** (with full orchestration) → 4. **Monitor & Correct** → 5. **Resolve or Reset**

---

## Step 1: Identify Task

**What**: Clearly define what you want to accomplish.

**Examples**:
- "Fix theme not saving to database"
- "Add user preference for notification sounds"
- "Refactor authentication module to use TypeScript"
- "Create diagnostic script for network failures"

**Check JAUmemory Collections**:
- Look for a "Bike Rack" collection (or similar task backlog collection) in JAUmemory
- This collection contains tasks/issues you want to tackle
- Query: `get_collection({ collection_id: "bike-rack-collection-id" })` or search for "bike rack" collection

**Say to Cursor** (if you need help clarifying):
```
I want to [describe task]. Help me identify the specific problem/feature and what success looks like.
```

---

## Step 2: Work with PM to Develop Plan

**What**: Use PM agent to create a plan with scaffolding - **DO NOT start coding yet**.

**Say to Cursor**:
```
PM, analyze this task: [describe task]

Create a plan with:
1. Problem analysis
2. Requirements
3. Scaffolding approach (file structure, interfaces, data flows)
4. Implementation strategy
5. Success criteria

DO NOT write code yet - only plan and scaffold.
```

**What PM Should Produce**:
- Problem analysis (check JAUmemory for existing problems)
- Requirements breakdown
- Scaffolding artifacts (file structure, interfaces, type definitions)
- Implementation strategy
- Diagnostic script requirements

**⚠️ CRITICAL**: If PM or any agent starts writing actual implementation code, **STOP IT IMMEDIATELY**:

**Say to Cursor**:
```
Stop. We're still in planning/scaffolding phase. Do not write implementation code yet. 
Focus on: [what you need - plan, scaffolding, interfaces, etc.]
```

**Why**: Planning and scaffolding first ensures you understand the problem, avoid duplication, and have a clear path forward before coding.

---

## Step 3: Review and Refine Plan

**What**: Review PM's plan and scaffolding. Refine until you're satisfied.

**Check for**:
- ✅ Clear problem statement
- ✅ Requirements are complete
- ✅ Scaffolding shows file structure and interfaces
- ✅ No duplicate code paths identified
- ✅ Diagnostic script requirements identified
- ✅ JAUmemory entry created/updated

**If plan needs refinement**:

**Say to Cursor**:
```
PM, refine the plan:
- [specific change 1]
- [specific change 2]
- [specific change 3]

Still no coding - just planning and scaffolding.
```

**Repeat until satisfied** with the plan and scaffolding.

---

## Step 4: Prepare System Prompt

**What**: Use text replacement to load the system prompt template.

### 4a. Load System Prompt

1. Type your shortcut (e.g., `;orch`) - it expands to full system prompt
2. Or copy from `SYSTEM_PROMPT.md`

### 4b. Replace Task Description

Replace `[describe bug clearly]` with your actual task/issue.

**Example**:
```
Objective:
Fix theme not saving to database when user toggles dark mode.
```

### 4c. Add Browser Console Logs (If Available)

**If you've already run the app in browser**:

1. Open browser DevTools (F12 or Cmd+Option+I)
2. Go to **Console** tab
3. Filter by "Errors" to see critical issues
4. Copy all relevant errors, warnings, and stack traces
5. Paste into the prompt under the task description

**If there's a diagnostic script**:

1. Load the diagnostic script in the browser console
2. Run it: `diagnoseIssue('issue-name')` or `diagnoseAll()`
3. Copy the diagnostic output
4. Paste into the prompt

**Format**:
```
Objective:
Fix theme not saving to database when user toggles dark mode.

Browser Console Logs:
[Paste console errors, warnings, diagnostic output here]
```

### 4d. Update Project Name

Replace `Active project = [your-project-name]` with your actual project name.

---

## Step 5: Submit Prompt

**What**: Send the complete prompt to Cursor.

**Before submitting, verify**:
- ✅ Task description is clear
- ✅ Browser console logs included (if available)
- ✅ Project name is correct
- ✅ All placeholders replaced

**Submit** the prompt to Cursor.

---

## Step 6: Monitor and Guide Execution

**What**: Watch the model output and intervene when needed.

### Watch for Unwanted Patterns

**Stop immediately if you see**:

1. **Backward compatibility for pre-launch product**:
   ```
   Stop. This is a pre-launch product. We don't need backward compatibility. 
   Remove the compatibility code and use only the new approach.
   ```

2. **Creating new code for something that already exists**:
   ```
   Stop. [Component/function] already exists at [location]. 
   Check for existing implementations first, then extend or refactor rather than creating duplicates.
   ```

3. **Not logging to JAUmemory**:
   ```
   Reminder: You must log this problem, solution, and verification to JAUmemory. 
   Create/update the memory entry now.
   ```

4. **Missing diagnostic script**:
   ```
   Reminder: This problem requires a diagnostic script to identify root cause. 
   Create the diagnostic script before implementing the solution.
   ```

5. **Skipping scaffolding**:
   ```
   Stop. We need to scaffold this first - create the file structure, interfaces, and type definitions 
   before writing implementation code.
   ```

### Positive Interventions

**If things are going well but you want to guide**:

```
Good progress. Make sure to:
1. Log this to JAUmemory with status update
2. Create diagnostic script for verification
3. Check for duplicate code before adding new functions
```

---

## Step 7: Handle Loops and Stuck Situations

**If you get into a loop or things aren't resolving**:

### Option 1: Revert in Cursor

**What**: Undo AI-generated changes in Cursor.

**How**: Use Cursor's AI undo feature to revert recent AI changes while keeping your manual edits.

**Say to Cursor**:
```
Revert the last AI changes. We're in a loop and need to reset.
```

### Option 2: Rollback to Previous Commit in Git

**What**: Use Git to rollback to a known good state.

**How**:
```bash
# See recent commits
git log --oneline -10

# Rollback to specific commit (creates new commit)
git revert <commit-hash>

# Or reset to specific commit (destructive - use carefully)
git reset --hard <commit-hash>
```

**Say to Cursor**:
```
We need to rollback. The current approach isn't working. 
Let's revert to commit [hash] and try a different approach.
```

### Option 3: Start Fresh Agent Thread

**What**: Start a new conversation thread to reset context.

**How**:
1. Start a new chat thread in Cursor
2. If you've been logging to JAUmemory, reference the memory:

**Say to Cursor**:
```
Starting fresh thread. We were working on [problem description]. 
The JAUmemory entry is [memoryId]. 
Recall that memory and continue from where we left off: [specific point to continue from].
```

**If you haven't been logging to JAUmemory**:

**Say to Cursor**:
```
Starting fresh thread. We were working on [problem description] but got stuck. 
First, search JAUmemory for any existing memories about this, then create a new memory entry 
for this problem with status "identified" and let's start fresh with a better approach.
```

---

## Step 8: Handle Long Thread Warnings

**If Cursor says the agent thread is too long**:

**If you've been logging to JAUmemory**:

1. Start a new thread
2. Reference the JAUmemory entry

**Say to Cursor**:
```
New thread. Continue work on problem [memoryId] from JAUmemory. 
We were at: [specific phase - e.g., "SD phase, implementing solution"]. 
Recall the memory and continue.
```

**If you haven't been logging**:

1. Start a new thread
2. Ask Cursor to retroactively create JAUmemory entries

**Say to Cursor**:
```
New thread. We were working on [problem] but the thread got too long. 
Please:
1. Create a JAUmemory entry summarizing what we've done so far
2. Continue from [specific point]
```

---

## Step 9: Repeat Until Conclusion

**What**: Iterate through steps 4-8 until the task is complete.

**Each iteration**:
1. Review what was accomplished
2. Check JAUmemory for status updates
3. Identify next steps
4. Prepare and submit new prompt if needed
5. Monitor and guide
6. Handle any issues

**Completion criteria**:
- ✅ Problem solved or feature implemented
- ✅ All tests pass
- ✅ Diagnostic scripts verify the fix
- ✅ JAUmemory entry updated to "solved"
- ✅ BLUE agent has approved
- ✅ Code committed with JAUmemory ID in commit message

---

## Quick Reference: Common Interventions

### Stop Coding, Plan First
```
Stop. We need to plan and scaffold first. Create the file structure, interfaces, and type definitions before writing implementation code.
```

### Remove Backward Compatibility
```
Stop. This is pre-launch. Remove backward compatibility code. Use only the new approach.
```

### Check for Duplicates
```
Stop. Before creating [component], search for existing implementations. 
Check [locations] and extend/refactor rather than duplicating.
```

### Log to JAUmemory
```
Reminder: Log this to JAUmemory. Create/update the memory entry with current status and findings.
```

### Create Diagnostic Script
```
Reminder: This problem needs a diagnostic script. Create it before implementing the solution.
```

### Reset Due to Loop
```
We're in a loop. Let's reset:
1. Revert recent AI changes
2. Recall JAUmemory entry [memoryId]
3. Try a different approach: [suggested approach]
```

---

## Workflow Checklist

Before starting:
- [ ] Task clearly identified
- [ ] Text replacement shortcut configured (`;orch`)
- [ ] Browser DevTools accessible (if debugging)
- [ ] JAUmemory access verified

During planning:
- [ ] PM creates plan with scaffolding
- [ ] Plan reviewed and refined
- [ ] No coding started yet
- [ ] JAUmemory entry created/updated

During execution:
- [ ] System prompt prepared with task and console logs
- [ ] Monitoring for unwanted patterns
- [ ] JAUmemory logging happening
- [ ] Diagnostic scripts created/executed

If stuck:
- [ ] Tried Cursor revert
- [ ] Considered Git rollback
- [ ] Started fresh thread if needed
- [ ] Referenced JAUmemory for continuity

At completion:
- [ ] Problem solved/feature implemented
- [ ] Tests pass
- [ ] Diagnostic scripts verify fix
- [ ] JAUmemory entry status = "solved"
- [ ] BLUE approved
- [ ] Committed with JAUmemory ID

