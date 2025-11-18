# JAUmemory Quickstart - Actionable Guide

Step-by-step commands and examples for using JAUmemory in the orchestration workflow.

## 1. Before Starting Any Task: Search for Existing Problems

**Action**: Always search JAUmemory first to avoid duplicate work.

**Command** (via Cursor or MCP):
```
recall({ query: "theme saving bug", limit: 10 })
```

**What to look for**:
- Similar problems already solved
- Related diagnostics that exist
- Known blind spots in this area

**If found**: Link to existing memory, don't create duplicate.

**If not found**: Proceed to create new memory (step 2).

---

## 2. Create Problem Memory When Starting Work

**When**: You've identified a new problem and confirmed it doesn't exist in JAUmemory.

**Command**:
```
remember({
  content: "Theme not saving to database in canopi extension",
  context: "User toggles theme in UI, but preference doesn't persist after refresh",
  tags: ["bug", "frontend", "preferences", "database"],
  importance: 0.8,
  metadata: {
    status: "identified",
    project: "canopi",
    affectedFiles: ["presence/utils/UserPreferencesManager.js", "presence/sidepanel.js"],
    impact: "Users lose theme preference on every refresh",
    rootCause: "Unknown - diagnostic needed"
  }
})
```

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

**Command**:
```
update({
  memoryId: "mem-abc-123",  // From step 2
  content: "Theme not saving - SOLUTION: Use immediate save (batch: false) in VisibilitySettingsManager.saveTheme()",
  importance: 0.8,
  metadata: {
    status: "proposed",
    solution: "Add { batch: false } to saveTheme() and ProfileManager.toggleTheme()",
    implementationPlan: "1. Update saveTheme() 2. Update toggleTheme() 3. Test persistence",
    riskAssessment: "LOW - simple parameter change",
    estimatedEffort: "15 minutes"
  }
})
```

**Key change**: `metadata.status` = `"proposed"`

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

**Command**:
```
update({
  memoryId: "mem-abc-123",
  content: "Theme saving FIXED - Added immediate save in saveTheme() and toggleTheme()",
  metadata: {
    status: "implemented",
    codeChanges: "Added { batch: false } parameter to save operations",
    filesModified: ["presence/utils/UserPreferencesManager.js", "presence/sidepanel.js"],
    testResults: "Theme persists after refresh - verified",
    diagnosticResults: "All sources now consistent"
  }
})
```

**Key change**: `metadata.status` = `"implemented"`

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
  projectContext: "canopi"
})
```

**Or link problem to agent**:
```
agent_memory({
  action: "link",
  agentId: "sd",
  memoryId: "mem-abc-123",
  category: "solution",
  projectContext: "canopi"
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

## 10. Consolidate Similar Memories (Monthly)

**When**: You have 5+ related memories in a collection.

**Command**:
```
consolidate_collection({
  collection_id: "coll-theme-789",
  title: "Theme Persistence Patterns - Q1 2025",
  summarize_only: false
})
```

**Result**: Creates a summary memory with insights, patterns, and lessons learned.

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
