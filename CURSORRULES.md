# Cursor Rules for Metalayer Initiative

## Field Naming Standardization (RED-LINE)

**CRITICAL**: In pre-release stages of development, **ALWAYS standardize field names rather than maintaining duplicate fields with different naming conventions**.

### Standard:
- **Use camelCase for ALL interface/JavaScript code** (e.g., `createdAt`, `parentId`, `pageId`, `userId`, `communityId`, `auraColor`)
- **Convert snake_case to camelCase immediately upon receipt from backend/Supabase**
- **Delete snake_case fields after conversion** - do NOT maintain both

### Prohibited Patterns:
- ❌ **DO NOT** maintain both `createdAt` and `created_at`
- ❌ **DO NOT** maintain both `parentId` and `parent_id`
- ❌ **DO NOT** maintain both `pageId` and `page_id`
- ❌ **DO NOT** maintain both `userId` and `user_id`
- ❌ **DO NOT** maintain both `communityId` and `community_id`
- ❌ **DO NOT** maintain both `conversationId` and `conversation_id`
- ❌ **DO NOT** maintain both `auraColor` and `aura_color`
- ❌ **DO NOT** add comments like "Also include X for compatibility" or "Also include X for backward compatibility"
- ❌ **DO NOT** add fallback patterns like `field || field_other` in display code

### Required Pattern:
```javascript
// ✅ CORRECT: Convert immediately, delete original
if (data.created_at && !data.createdAt) {
  data.createdAt = data.created_at;
  delete data.created_at;
}

// ✅ CORRECT: Use only camelCase
formatMessageTime(message.createdAt)

// ❌ WRONG: Maintaining both
{
  createdAt: data.created_at,
  created_at: data.created_at // Also include for compatibility
}

// ❌ WRONG: Fallback in display
formatMessageTime(message.createdAt || message.created_at)
```

### Enforcement:
- This is a **RED-LINE** policy - violations block release
- All field name conversions must happen at the **interface boundary** (API/Supabase → JavaScript)
- Once converted to camelCase, use **ONLY camelCase** throughout the codebase

## Extension Distribution Cleanliness (RED-LINE)

**CRITICAL**: The `presence/` directory is the **extension distribution** that gets packaged and deployed. It must contain ONLY runtime files.

### Prohibited in Distribution:
- ❌ **DO NOT** create `.md` files in `presence/` root - put documentation in `docs/` or parent directory
- ❌ **DO NOT** put TypeScript source files (`.ts`) in `presence/` root - they belong in `src/` and compile to `dist/`
- ❌ **DO NOT** create test files (`*test*.js`, `*test*.ts`) in `presence/` root - use `tests/` subdirectory
- ❌ **DO NOT** create temporary files (`.tmp`, `.log`, `CLEANUP_LOG.json`) in distribution
- ❌ **DO NOT** create build scripts (`.sh`) in `presence/` root - use `scripts/` subdirectory
- ❌ **DO NOT** create SQL migration files (`.sql`) in distribution
- ❌ **DO NOT** create diagnostic/debug scripts (`DIAGNOSTIC_*.js`, `console_*.js`) in distribution
- ❌ **DO NOT** create status/progress files (`*_STATUS*.md`, `*_PROGRESS*.md`, `MIGRATION_*.md`) in distribution
- ❌ **DO NOT** leave stale tests or diagnostics in place “just in case” – retire or archive them
- ❌ **DO NOT** resurrect files that were previously archived without re-review

### Required Pattern:
```bash
# ✅ CORRECT: Source files OUTSIDE presence/, compiled directly to presence/
src/presence/        # TypeScript source (OUTSIDE distribution)
  features/
  utils/
presence/            # Distribution (compiled output goes here)
  core/              # Compiled JavaScript (IN distribution)
  features/          # Compiled JavaScript (IN distribution)
  utils/             # Compiled JavaScript (IN distribution)
  manifest.json      # Runtime file (IN distribution)
  sidepanel.html     # Runtime file (IN distribution)
  sidepanel.js       # Runtime file (IN distribution)

# ✅ CORRECT: Documentation in docs/ or parent
docs/
  MIGRATION_PROGRESS.md
  ORCHESTRATION_REPORTS/

# ❌ WRONG: Polluting distribution
presence/
  src/                      # Should be in parent src/presence/
  dist/                     # Should compile directly to presence/ root
  MIGRATION_PROGRESS.md     # Should be in docs/
  test_something.js         # Should be in tests/
  cleanup.sh               # Should be in scripts/
```

### Build Process:
1. **Always compile TypeScript**: `src/presence/` → `presence/` (use `npm run build:extension` or `scripts/build-distribution.sh`)
2. **Run cleanup before distribution**: `scripts/cleanup-distribution.sh` removes non-runtime files (including `src/` and `dist/` if present)
3. **Verify distribution**: Only runtime files (`.js`, `.html`, `.css`, `manifest.json`, compiled directories, assets) should remain
4. **Documentation discipline**: If you need notes/diagnostics, output them in console/JAUmemory, store structured docs under `docs/` or `/archive/`, and delete the temp file from distribution immediately after use.
5. **Archive workflow**: Move any “maybe later” scripts/tests into `/archive/{original-path}/` with a README explaining why it lives there. Reference the archive entry inside JAUmemory for traceability.

### Enforcement:
- Distribution pollution is a **RED-LINE** - it increases bundle size and confuses deployment
- Before committing changes to `presence/`, verify no `.md`, `.ts`, `.sh`, or test files were added to root
- Use `scripts/build-distribution.sh` to ensure clean builds
- BLUE cannot approve if non-runtime artifacts remain inside the extension package.

## TypeScript Migration Context & Error Prevention

### Codebase Architecture
- **122 TypeScript files** - Large codebase, always check related files before making changes
- **Window Globals**: Heavy reliance on `window` object for global state (temporary during migration)
  - `window.currentUser`: Current authenticated user (User | null) - **ALWAYS null-check before access**
  - `window.currentVisibilityData`: Active users on current page (User[]) - **May be undefined on init**
  - `window.currentVisibilityDataUnfiltered`: All visibility data (unfiltered)
  - `window.api`: API client instance - **May be undefined if not initialized**
  - **Pattern**: Always check: `if (window.currentUser) { /* use it */ }`
  - **Future**: Will migrate to proper state management (Redux/Zustand)

### Common Runtime Error Categories (TypeScript Won't Catch)

#### 1. **DOM Access Errors**
- **Pattern**: `document.getElementById()` returns `HTMLElement | null`
- **Required**: Always null-check before accessing properties
  ```typescript
  // ✅ CORRECT
  const element = document.getElementById('menu');
  if (element) {
    element.style.display = 'none';
  }
  
  // ❌ WRONG - Will crash if element doesn't exist
  document.getElementById('menu').style.display = 'none';
  ```

#### 2. **Event Handler Issues**
- **Pattern**: Event handlers must be stored for cleanup to prevent memory leaks
- **Required**: Always store handler references and remove them in dispose/cleanup
  ```typescript
  // ✅ CORRECT
  private clickHandler?: (e: Event) => void;
  
  setup() {
    this.clickHandler = (e: Event) => { /* ... */ };
    element.addEventListener('click', this.clickHandler);
  }
  
  dispose() {
    if (this.clickHandler) {
      element.removeEventListener('click', this.clickHandler);
      this.clickHandler = undefined;
    }
  }
  
  // ❌ WRONG - Memory leak, handler never removed
  element.addEventListener('click', (e) => { /* ... */ });
  ```

#### 3. **Event Target Type Narrowing**
- **Pattern**: `e.target` is `EventTarget | null`, not `HTMLElement`
- **Required**: Use type guards for event targets
  ```typescript
  // ✅ CORRECT
  if (e.target instanceof HTMLInputElement) {
    console.log(e.target.value); // TypeScript knows it's HTMLInputElement
  }
  
  // ❌ WRONG - TypeScript error or runtime undefined
  console.log(e.target.value); // EventTarget doesn't have 'value'
  ```

#### 4. **Async/Await Error Handling**
- **Pattern**: Async functions must handle errors or they'll be swallowed
- **Required**: Always wrap async operations in try/catch
  ```typescript
  // ✅ CORRECT
  button.addEventListener('click', async () => {
    try {
      await saveData();
      showSuccess();
    } catch (error) {
      console.error('Save failed:', error);
      showError(error);
    }
  });
  
  // ❌ WRONG - Errors silently fail
  button.addEventListener('click', async () => {
    await saveData(); // If this fails, user sees nothing
  });
  ```

#### 5. **Window Global Null Checks**
- **Pattern**: Window globals may be undefined during initialization
- **Required**: Always check before accessing
  ```typescript
  // ✅ CORRECT
  if (window.currentUser && window.currentUser.id) {
    updateUI(window.currentUser);
  }
  
  // ❌ WRONG - Crashes if currentUser is null
  updateUI(window.currentUser); // May be null!
  ```

#### 6. **Promise Rejection Handling**
- **Pattern**: Unhandled promise rejections cause silent failures
- **Required**: Always handle promise rejections
  ```typescript
  // ✅ CORRECT
  fetch(url)
    .then(response => response.json())
    .then(data => processData(data))
    .catch(error => {
      console.error('Request failed:', error);
      handleError(error);
    });
  
  // ❌ WRONG - Unhandled rejection
  fetch(url).then(response => response.json()); // No error handling
  ```

### Type Safety Patterns

#### Avoid `any` Types
- **Use `unknown` + type guards** instead of `any`
  ```typescript
  // ✅ CORRECT
  function processData(data: unknown) {
    if (data && typeof data === 'object' && 'id' in data) {
      console.log((data as { id: string }).id);
    }
  }
  
  // ❌ WRONG - Loses type safety
  function processData(data: any) {
    console.log(data.id); // No type checking
  }
  ```

#### Avoid Unsafe Type Assertions
- **Use type guards** instead of `as` casts
  ```typescript
  // ✅ CORRECT
  if (user && 'id' in user && typeof user.id === 'string') {
    console.log(user.id); // TypeScript knows it's safe
  }
  
  // ❌ WRONG - May crash at runtime
  console.log((user as User).id); // Assumes user is User, may be null
  ```

### Error Investigation Workflow

When investigating an error:
1. **TypeScript compilation**: Does it compile? (`npm run build:presence`)
2. **Runtime error**: What's the actual error message in console?
3. **Stack trace**: Where does it originate? (Check line numbers)
4. **State check**: What's the value of relevant window globals? (Add `console.log`)
5. **Timing**: Does it happen on load, after interaction, or randomly?
6. **Reproduction**: Can you reproduce it consistently?

### Code Review Checklist

Before submitting code:
- [ ] All `document.getElementById()` calls have null checks
- [ ] Event handlers are stored and properly cleaned up
- [ ] Async functions have try/catch error handling
- [ ] Window globals are null-checked before access
- [ ] Type assertions use type guards, not `as` casts
- [ ] No `any` types (use `unknown` + guards)
- [ ] Event targets are properly narrowed with `instanceof`
- [ ] Promise rejections are handled with `.catch()` or try/catch

### Context Loading Strategy

When fixing errors or adding features:
1. **Read related files first**: Understand the module's dependencies
2. **Check window globals**: See what global state is used (`grep -r "window\." src/`)
3. **Review event handlers**: Check for cleanup patterns
4. **Examine async flows**: Trace promise chains and async/await
5. **Check type definitions**: Review `src/types/index.ts` for available types

### Memory Storage (JAUmemory)

Store important learnings:
- Common error patterns and their fixes
- Window global initialization order (what depends on what)
- Event handler cleanup patterns that work
- Type guard patterns for common types
- API response shapes and normalization points
- DOM element IDs and their purposes
- Module dependencies and initialization order

See `TYPESCRIPT_MIGRATION_INSIGHTS.md` for detailed analysis of remaining error categories.

## Architecture & Collaboration Guardrails (RED-LINE)

- **ES Modules only**: Use TypeScript + ES6 module syntax (`import`/`export`). No CommonJS or implicit globals.
- **Modular every change**: Keep features decomposed into composable modules; never pile logic into monolith files.
- **No pre-launch backward compatibility shims**: Remove duplicate code paths or legacy fallbacks instead of introducing compatibility branches. If absolutely required, gain PM + BLUE approval and document in JAUmemory.
- **Duplicate detection**: Before adding new functionality, search for similar utilities/components and extend them; do not create parallel implementations.
- **Plan → Scaffold → Build**: Every task must document planning notes, scaffolding artifacts, and final implementation steps (in JAUmemory + PR/commit).
- **Always log to JAUmemory**: Problem statement, diagnostics, solution, verification, blind-spot notes, red-line outcomes, and final commit hash must live in JAUmemory.
- **Avoid fallbacks**: No `value || fallbackValue` hacks masking data quality. Fix the source, document diagnostics, and remove redundant checks.
- **Commit on resolution**: Once BLUE approves and verification passes, produce a final commit tagged/annotated with the JAUmemory problem ID.
- **Unify repeated logic**: When you see duplicated code paths, extract shared helpers/modules instead of copy-pasting. Document the reuse decision in JAUmemory.

## Parallel Orchestration Policy

- When a task is **time-consuming yet partitionable** (typical low-to-medium difficulty refactors, documentation cleanup, diagnostic conversions, etc.), the orchestrator must ask the user whether to spin up **8–10 parallel Orch sessions**.
- If approved, provide each Orch with:
  - A scoped prompt chunk covering roughly equal effort
  - Clear ownership of files/modules
  - Shared references to diagnostics, JAUmemory entries, and guardrails
- Never over-parallelize tasks that depend on strict sequencing or single-owner context.
