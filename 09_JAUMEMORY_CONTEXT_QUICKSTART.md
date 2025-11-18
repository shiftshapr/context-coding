# JAUmemory Quickstart - Actionable Guide

Step-by-step commands and examples for using JAUmemory in the orchestration workflow.

## Setup: Configure Your Cursor Environment

### Step 1: Authenticate with JAUmemory

**Say to Cursor**:
```
I need to authenticate with JAUmemory. Can you help me log in using the MCP login function?
```

**Or if you have credentials ready**:
```
Authenticate me with JAUmemory. My username is [your-username] and email is [your-email].
```

**Cursor will**:
- Call `mcp_jaumemory_mcp_login()` with your credentials
- Provide a link to approve in your browser
- Wait for you to click and approve
- Complete authentication with the token you receive

**After approval, say**:
```
Complete JAUmemory authentication with token [paste-token-here]
```

### Step 2: Verify JAUmemory is Working

**Say to Cursor**:
```
Test JAUmemory by listing all available agents
```

**Or**:
```
Can you recall any memories about "preferences" in the [project-name] project?
```

**Expected response**: Cursor should list agents or return memory results. If it works, you're ready.

### Step 3: Test Creating a Memory

**Say to Cursor**:
```
Create a test memory in JAUmemory with content "Testing setup", tags ["test"], and importance 0.1
```

**Expected**: Memory created successfully with a memoryId returned.

### Step 4: Verify You Can Query Memories

**Say to Cursor**:
```
Search JAUmemory for any memories tagged with "test"
```

**Expected**: Your test memory appears in results.

**If any step fails**: Check that JAUmemory MCP server is configured in Cursor settings and that you have valid credentials.

---

## 1. Before Starting Any Task: Search for Existing Problems

**Action**: Always search JAUmemory first to avoid duplicate work.

**Check Collections First**:
- Look for a **"Bike Rack"** collection - this contains tasks/issues you want to tackle
- Query: `list_collections()` to see all collections
- Or: `get_collection({ collection_id: "bike-rack-id" })` if you know the ID

**Search for Existing Problems**:

**Say to Cursor**:
```
Search JAUmemory for any existing problems about "theme saving" in the [project-name] project
```

**Or more specific**:
```
Recall memories about theme persistence bugs, limit to 10 results
```

**What to look for**:
- Similar problems already solved
- Related diagnostics that exist
- Known blind spots in this area
- Tasks in the Bike Rack collection

**If found**: Say to Cursor:
```
Link this new problem to the existing memory [memoryId] and use that instead of creating a duplicate
```

**If not found**: Proceed to create new memory (step 2).

---

## 2. Create Problem Memory When Starting Work

**When**: You've identified a new problem and confirmed it doesn't exist in JAUmemory.

**Say to Cursor**:
```
Create a new problem memory in JAUmemory:
- Content: "Theme not saving to database in [project-name] extension"
- Context: "User toggles theme in UI, but preference doesn't persist after refresh"
- Tags: bug, frontend, preferences, database
- Importance: 0.8
- Status: identified
- Project: [project-name]
- Affected files: presence/utils/UserPreferencesManager.js, presence/sidepanel.js
- Impact: Users lose theme preference on every refresh
```

**Cursor will create the memory** with proper structure. **Save the memoryId** it returns - you'll need it for updates.

**Required fields**:
- `content`: Clear problem description
- `context`: What's happening, when it occurs
- `tags`: At least 3-4 tags (component, type, severity)
- `importance`: 0.0-1.0 (0.8+ = critical)
- `metadata.status`: Always start with `"identified"`

**Output**: You'll get a `memoryId` - **save this**, you'll update it throughout the workflow.

---

## 3. Update Memory When Proposing Solution

**When**: SD agent has designed a solution.

**Say to Cursor**:
```
Update memory mem-abc-123 with:
- New content: "Theme not saving - SOLUTION: Use immediate save (batch: false) in VisibilitySettingsManager.saveTheme()"
- Status: proposed
- Solution: "Add { batch: false } to saveTheme() and ProfileManager.toggleTheme()"
- Implementation plan: "1. Update saveTheme() 2. Update toggleTheme() 3. Test persistence"
- Risk: LOW - simple parameter change
- Estimated effort: 15 minutes
```

**Key change**: Status moves from `"identified"` to `"proposed"`

---

## 4. Create Diagnostic Script (Required)

**When**: Before implementing solution (SD phase).

**Action**: Create diagnostic script using the framework.

**File**: `/presence/utils/ROOT_CAUSE_DIAGNOSTIC_FRAMEWORK.js`

**Example code**:
```javascript
diagnosticFramework.register('theme-persistence', async () => {
  const results = {
    timestamp: new Date().toISOString(),
    chromeStorage: null,
    database: null,
    userPreferences: null,
    inconsistencies: []
  };
  
  // Check Chrome storage
  const chromeData = await chrome.storage.local.get(['theme']);
  results.chromeStorage = chromeData.theme;
  
  // Check database (via API)
  const user = await window.api.getUser(window.currentUser.id);
  results.database = user.preferences?.theme;
  
  // Check UserPreferencesManager
  if (window.userPreferencesManager) {
    results.userPreferences = await window.userPreferencesManager.getPreference('theme');
  }
  
  // Find inconsistencies
  if (results.chromeStorage !== results.database) {
    results.inconsistencies.push('Chrome storage != database');
  }
  
  console.log('Theme Diagnostic Results:', results);
  return results;
}, 'Checks theme persistence across Chrome storage, database, and UserPreferencesManager');
```

**Then update memory with diagnostic ID**:
```
update({
  memoryId: "mem-abc-123",
  metadata: {
    diagnosticScript: "theme-persistence",
    diagnosticLocation: "/presence/utils/ROOT_CAUSE_DIAGNOSTIC_FRAMEWORK.js"
  }
})
```

---

## 5. Update Memory After Implementation

**When**: Code is written and tested.

**Say to Cursor**:
```
Update memory mem-abc-123:
- Status: implemented
- Content: "Theme saving FIXED - Added immediate save in saveTheme() and toggleTheme()"
- Code changes: "Added { batch: false } parameter to save operations"
- Files modified: presence/utils/UserPreferencesManager.js, presence/sidepanel.js
- Test results: "Theme persists after refresh - verified"
- Diagnostic results: "All sources now consistent"
```

**Key change**: Status moves from `"proposed"` to `"implemented"`

---

## 6. Update Memory After Verification

**When**: TEST agent confirms fix works, BLUE approves.

**Command**:
```
update({
  memoryId: "mem-abc-123",
  content: "Theme saving SOLVED - Immediate save prevents batching delay",
  metadata: {
    status: "solved",
    verificationResults: "Theme persists correctly after refresh",
    testOutcomes: "All tests pass",
    lessonsLearned: "Batched saves can cause persistence issues - use immediate saves for critical preferences",
    commitHash: "abc123def456"
  }
})
```

**Key change**: `metadata.status` = `"solved"` (or `"failed"` if fix didn't work)

---

## 7. Record Blind-Spot Findings

**When**: BLINDSPOT agent identifies edge cases.

**Command**:
```
remember({
  content: "Theme toggle race condition: rapid clicks can cause inconsistent state",
  context: "User clicks theme toggle 5 times quickly, only last state may save",
  tags: ["blindspot", "race-condition", "ui", "preferences"],
  importance: 0.6,
  metadata: {
    triggerConditions: "Rapid UI interactions within 500ms",
    mitigation: "Debounce theme toggle handler",
    component: "ProfileManager.toggleTheme()",
    relatedProblem: "mem-abc-123"
  }
})
```

**Then add to collection**:
```
create_collection({ name: "Blind-Spot Radar" })
add_to_collection({ collection_id: "coll-xyz", memory_id: "mem-blindspot-456" })
```

---

## 8. Link Related Memories

**When**: You find connections between problems.

**Command**:
```
// Link blind-spot to original problem
agent_memory({
  action: "link",
  agentId: "blindspot",
  memoryId: "mem-blindspot-456",
  category: "learning",
  projectContext: "[project-name]"
})
```

**Or link problem to agent**:
```
agent_memory({
  action: "link",
  agentId: "sd",
  memoryId: "mem-abc-123",
  category: "solution",
  projectContext: "[project-name]"
})
```

---

## 9. Create Collections for Related Work

**When**: Multiple memories relate to the same theme.

**Command**:
```
// Create collection
create_collection({
  name: "Theme-Related Problems",
  description: "All issues related to theme persistence and UI"
})

// Add memories to collection
add_to_collection({
  collection_id: "coll-theme-789",
  memory_id: "mem-abc-123"
})
add_to_collection({
  collection_id: "coll-theme-789",
  memory_id: "mem-blindspot-456"
})
```

**View collection**:
```
get_collection({ collection_id: "coll-theme-789" })
```

---

## 10. Automatic Learning Phase (Built into Workflow)

**When**: Automatically happens after every bug fix (BLUE agent executes this)

**What happens automatically** (you don't need to do anything):
1. **Pattern Identification**: System searches for similar issues in codebase and JAUmemory
2. **Prevention Strategy**: Creates prevention patterns and updates agent memories
3. **Automatic Detection**: Registers error signatures and code patterns for future auto-detection
4. **Knowledge Consolidation**: Consolidates related memories into pattern insights

**Collections created automatically**:
- **"Pattern Library"** - Reusable patterns for automatic issue detection
- **"Blind-Spot Patterns"** - Patterns that were blind spots
- **"Diagnostic Patterns"** - Reusable diagnostic scripts

**How it works**:
- After BLUE confirms a fix, the learning phase automatically:
  - Searches for similar code patterns in your codebase
  - Searches JAUmemory for similar problems
  - Creates pattern memories with error signatures and solutions
  - Updates agent memories so they recognize patterns
  - Registers diagnostic scripts as reusable patterns
  - Proposes guardrail updates if needed

**You'll see**: A "Learning Phase Report" in the final output showing:
- Similar issues found
- Pattern created/updated
- Prevention strategies documented
- Diagnostic patterns registered

**To view patterns later**:
```
// List all collections
list_collections()

// Get Pattern Library
get_collection({ collection_id: "pattern-library-id" })

// Search for patterns
recall({ query: "pattern", tags: ["pattern", "prevention"] })
```

## 11. Consolidate Similar Memories (Monthly)

**When**: You have 5+ related memories in a collection (or the learning phase identifies them).

**Command**:
```
consolidate_collection({
  collection_id: "coll-theme-789",
  title: "Theme Persistence Patterns - Q1 2025",
  summarize_only: false
})
```

**Result**: Creates a summary memory with insights, patterns, and lessons learned.

**Note**: The automatic learning phase may consolidate memories automatically if it finds 2+ similar problems.

---

## Quick Reference: Memory Status Flow

```
identified → proposed → implemented → solved/failed
```

**Update status at each workflow phase**:
- PM: `identified`
- SD: `proposed`
- SD (after coding): `implemented`
- BLUE (after verification): `solved` or `failed`

---

## Quick Reference: Common Queries

**Find problems by component**:
```
recall({ query: "preferences bug", tags: ["frontend"], limit: 20 })
```

**Find unsolved problems**:
```
recall({ query: "status:identified OR status:proposed", limit: 50 })
```

**Find agent's work**:
```
agent_memory({ action: "recall", agentId: "sd", limit: 20 })
```

**Find blind spots**:
```
recall({ query: "blindspot", tags: ["race-condition"], limit: 10 })
```

---

## Common Mistakes to Avoid

❌ **Creating duplicate memories** - Always search first
❌ **Forgetting to update status** - Memory stuck in `identified` forever
❌ **Not linking related memories** - Patterns never emerge
❌ **Skipping diagnostic scripts** - Can't verify root cause
❌ **Not tagging properly** - Can't find memories later
❌ **Forgetting to consolidate** - Knowledge stays fragmented

✅ **Always**: Search → Create → Update → Link → Consolidate
