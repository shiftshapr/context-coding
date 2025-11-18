# Agent 7: Types, Global, & Remaining Files

**Priority:** MEDIUM  
**Objective:** Strategic `any` reduction in types/global + remaining files (133 `any` types → target: ~30)

---

## 📁 Assigned Files

**Primary:**
1. `presence/src/types/global.d.ts` (39 `any` - strategic reduction)
2. `presence/src/types/index.ts` (17 `any`)

**Secondary (10+ files, ~77 `any`):**
3. `presence/src/features/APIModule.ts` (10 `any`)
4. `presence/src/utils/UserPreferencesManager.ts` (6 `any`)
5. `presence/src/utils/ReplyLoader.ts` (4 `any`)
6. `presence/src/features/CommunitiesModule.ts` (5 `any`)
7. `presence/src/features/UserHoverModal.ts` (5 `any`)
8. `presence/src/utils/patches/ChatLoadingOverlayPatch.ts` (5 `any`)
9. `presence/src/utils/provenance/init.ts` (4 `any`)
10. Plus remaining smaller files (see full list in main prompt)

---

## 🎯 Tasks

### 1. global.d.ts (STRATEGIC REDUCTION)

**Current Issues:**
- Many `?: any` for integration objects
- Diagnostic functions not fully typed
- Some truly dynamic cases that can be more specific

**Actions:**
1. **Replace integration `any` types:**
   - Create interfaces for integration objects:
     ```typescript
     interface AurasIntegration {
       updateAura?: (userId: string, auraColor: string) => void;
       getAura?: (userId: string) => Promise<string | null>;
     }
     
     interface RobustIntegration {
       sendMessage?: (message: Message) => Promise<void>;
       // ... other methods
     }
     ```
   - Replace `aurasIntegration?: any` → `aurasIntegration?: AurasIntegration`
   - Do the same for `robustIntegration`, `reactionsIntegration`, etc.

2. **Type diagnostic functions:**
   - Use existing diagnostic result types from `utils/diagnostics/types.ts`
   - Replace `runMessageDisplayDiagnostic?: () => Promise<any>` → `runMessageDisplayDiagnostic?: () => Promise<MessageDisplayDiagnosticResult>`
   - Do the same for other diagnostic functions

3. **Keep `any` for truly dynamic cases:**
   - Keep `[key: string]: any` for dynamic properties
   - Keep `any` for truly generic/unknown types
   - Document why `any` is kept in comments

**Target:** Reduce from 39 to 20-25 `any` (strategic reduction)

---

### 2. types/index.ts

**Current Issues:**
- Some `any` in type exports
- Type unions that could be more specific

**Actions:**
1. **Review all type exports:**
   - Ensure all exported types are specific (not `any`)
   - Remove `any` from type unions where possible
   - Add missing type exports if needed

2. **Type re-exports:**
   - Ensure re-exports from other type files are properly typed
   - No `any` in exported types

**Target:** Reduce from 17 to <5 `any`

---

### 3. APIModule.ts

**Current Issues:**
- API responses not typed
- API options not typed

**Actions:**
1. **Type API responses:**
   - Use `ApiResponse<T>` from `types/api.ts`
   - Replace `response: any` → `response: ApiResponse<DataType>`
   - Type all API method return types

2. **Type API options:**
   - Use `APIRequestOptions` from `types/api.ts`
   - Replace `options?: any` → `options?: APIRequestOptions`

**Success:** All API operations use typed responses

---

### 4. UserPreferencesManager.ts

**Current Issues:**
- Some `any` in preference value handling
- Already partially typed, finish the job

**Actions:**
1. **Complete preference typing:**
   - Ensure `PreferenceValue` type is used everywhere
   - Replace any remaining `any` with `PreferenceValue`
   - Type all preference-related methods

**Success:** All preferences fully typed

---

### 5. Remaining Files (ReplyLoader, CommunitiesModule, etc.)

**Actions:**
1. **Type each file systematically:**
   - `ReplyLoader.ts`: Type reply data with `Message` type
   - `CommunitiesModule.ts`: Type community data with `Community` interface
   - `UserHoverModal.ts`: Type user data with `User` type
   - `ChatLoadingOverlayPatch.ts`: Type patch data
   - `provenance/init.ts`: Type initialization data

2. **Create missing types:**
   - Create `Community` interface if not exists
   - Create patch data interfaces
   - Use existing types where available

**Success:** All remaining files typed

---

## ✅ RED-LINE Compliance

- ❌ NO snake_case in type names
- ❌ NO direct `window.property = value`
- ❌ NO `(window as any)`
- ✅ USE camelCase for all properties
- ✅ STRATEGIC use of `any` only for truly dynamic cases
- ✅ Document why `any` is kept in comments

---

## 🧪 Verification

After completion, run:
```bash
cd /home/ubuntu/metalayer-initiative
npx tsc --noEmit
grep -r ": any" presence/src/types/ presence/src/features/APIModule.ts presence/src/utils/UserPreferencesManager.ts presence/src/utils/ReplyLoader.ts presence/src/features/CommunitiesModule.ts presence/src/features/UserHoverModal.ts presence/src/utils/patches/ChatLoadingOverlayPatch.ts presence/src/utils/provenance/init.ts
```

**Target:** 
- `global.d.ts`: 20-25 `any` (strategic)
- `types/index.ts`: <5 `any`
- Other files: <5 `any` each
- **Total: ~30 `any` remaining**

---

## 📝 Notes

- **STRATEGIC APPROACH:** `global.d.ts` will always have some `any` for truly dynamic cases - that's OK
- Check existing type definitions in `presence/src/types/`
- Use `ApiResponse<T>` from `types/api.ts`
- Use `Message`, `User`, `Preferences` from `types/index.ts`
- Test compilation after each file
- Document why `any` is kept in `global.d.ts`


