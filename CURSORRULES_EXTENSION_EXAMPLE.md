# Extension-Specific Cursor Rules Example

**NOTE**: This file contains rules specific to **browser extension development**. Only use these if you're building a Chrome/Firefox/Edge extension. For other project types, use `CURSORRULES_GENERIC.md` instead.

## Extension Distribution Cleanliness (RED-LINE)

**CRITICAL**: The distribution directory (e.g., `dist/`, `build/`, or `extension/`) that gets packaged and deployed must contain ONLY runtime files.

### Prohibited in Distribution:
- ❌ **DO NOT** create `.md` files in distribution root - put documentation in `docs/` or parent directory
- ❌ **DO NOT** put TypeScript source files (`.ts`) in distribution - they belong in `src/` and compile to distribution
- ❌ **DO NOT** create test files (`*test*.js`, `*test*.ts`) in distribution - use `tests/` subdirectory
- ❌ **DO NOT** create temporary files (`.tmp`, `.log`, `CLEANUP_LOG.json`) in distribution
- ❌ **DO NOT** create build scripts (`.sh`) in distribution root - use `scripts/` subdirectory
- ❌ **DO NOT** create SQL migration files (`.sql`) in distribution
- ❌ **DO NOT** create diagnostic/debug scripts (`DIAGNOSTIC_*.js`, `console_*.js`) in distribution
- ❌ **DO NOT** create status/progress files (`*_STATUS*.md`, `*_PROGRESS*.md`, `MIGRATION_*.md`) in distribution
- ❌ **DO NOT** leave stale tests or diagnostics in place "just in case" – retire or archive them
- ❌ **DO NOT** resurrect files that were previously archived without re-review

### Required Pattern:
```bash
# ✅ CORRECT: Source files OUTSIDE distribution, compiled directly to distribution
src/              # TypeScript source (OUTSIDE distribution)
  features/
  utils/
dist/             # Distribution (compiled output goes here)
  features/        # Compiled JavaScript (IN distribution)
  utils/          # Compiled JavaScript (IN distribution)
  manifest.json    # Runtime file (IN distribution)
  popup.html       # Runtime file (IN distribution)
  popup.js         # Runtime file (IN distribution)

# ✅ CORRECT: Documentation in docs/ or parent
docs/
  MIGRATION_PROGRESS.md
  ORCHESTRATION_REPORTS/

# ❌ WRONG: Polluting distribution
dist/
  src/                      # Should be in parent src/
  MIGRATION_PROGRESS.md     # Should be in docs/
  test_something.js         # Should be in tests/
  cleanup.sh               # Should be in scripts/
```

### Build Process:
1. **Always compile TypeScript**: `src/` → `dist/` (use `npm run build` or your build script)
2. **Run cleanup before distribution**: Remove non-runtime files (including `src/` and test files if present)
3. **Verify distribution**: Only runtime files (`.js`, `.html`, `.css`, `manifest.json`, compiled directories, assets) should remain
4. **Documentation discipline**: If you need notes/diagnostics, output them in console/JAUmemory, store structured docs under `docs/` or `/archive/`, and delete the temp file from distribution immediately after use.
5. **Archive workflow**: Move any "maybe later" scripts/tests into `/archive/{original-path}/` with a README explaining why it lives there. Reference the archive entry inside JAUmemory for traceability.

### Enforcement:
- Distribution pollution is a **RED-LINE** - it increases bundle size and confuses deployment
- Before committing changes to distribution, verify no `.md`, `.ts`, `.sh`, or test files were added
- Use build scripts to ensure clean builds
- BLUE cannot approve if non-runtime artifacts remain inside the extension package.

## Extension-Specific TypeScript Context

### Extension Architecture
- **Manifest files**: Always validate `manifest.json` structure matches extension platform requirements
- **Content Scripts**: Ensure proper isolation and message passing between content scripts and background
- **Background Workers**: Use service workers (Manifest V3) or background pages (Manifest V2) appropriately
- **Popup/Options Pages**: Handle state persistence across popup opens/closes
- **Storage APIs**: Use `chrome.storage` or `browser.storage` for extension-specific data

### Extension-Specific Error Patterns

#### Content Script Isolation
- **Pattern**: Content scripts run in isolated world, can't directly access page JavaScript
- **Required**: Use `window.postMessage` or `chrome.runtime.sendMessage` for communication
  ```typescript
  // ✅ CORRECT: Message passing
  chrome.runtime.sendMessage({ action: 'getData' }, (response) => {
    // Handle response
  });
  
  // ❌ WRONG: Direct access (won't work)
  window.pageVariable // Not accessible from content script
  ```

#### Storage API Usage
- **Pattern**: `chrome.storage` is async, returns results in callback or promise
- **Required**: Always handle async storage operations
  ```typescript
  // ✅ CORRECT
  chrome.storage.local.get(['key'], (result) => {
    if (chrome.runtime.lastError) {
      console.error(chrome.runtime.lastError);
      return;
    }
    useData(result.key);
  });
  
  // ❌ WRONG - Synchronous access
  const data = chrome.storage.local.get('key'); // Returns undefined
  ```

#### Manifest Permissions
- **Pattern**: Extension permissions must be declared in `manifest.json`
- **Required**: Always check required permissions before using APIs
  ```typescript
  // ✅ CORRECT: Check permissions
  if (chrome.permissions && chrome.permissions.contains) {
    chrome.permissions.contains({ permissions: ['tabs'] }, (hasPermission) => {
      if (hasPermission) {
        // Use tabs API
      }
    });
  }
  ```

### Extension Build Checklist

Before packaging extension:
- [ ] No TypeScript source files in distribution
- [ ] No test files in distribution
- [ ] No markdown/documentation files in distribution
- [ ] No build scripts in distribution
- [ ] `manifest.json` is valid and complete
- [ ] All assets referenced in manifest exist
- [ ] Content security policy (CSP) is properly configured
- [ ] Extension loads without errors in browser
- [ ] All permissions are justified and minimal

