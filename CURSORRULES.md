# Cursor Rules - Index

This directory contains cursor rules templates. Choose the appropriate file(s) for your project:

## For All Projects
- **`CURSORRULES_GENERIC.md`** – Universal rules that apply to any TypeScript/JavaScript project
  - Field naming standards
  - TypeScript safety patterns
  - Architecture guardrails
  - Error handling patterns
  - JAUmemory integration

## For Browser Extensions Only
- **`CURSORRULES_EXTENSION_EXAMPLE.md`** – Additional rules specific to Chrome/Firefox/Edge extensions
  - Distribution cleanliness
  - Extension-specific TypeScript patterns
  - Manifest and permissions handling
  - Content script isolation

## Usage

1. **Start with generic rules**: Copy `CURSORRULES_GENERIC.md` as your base `.cursorrules` file
2. **Add extension rules if needed**: If building a browser extension, also include relevant sections from `CURSORRULES_EXTENSION_EXAMPLE.md`
3. **Customize for your project**: Add project-specific guardrails, naming conventions, or architecture patterns

## Setup with Cursor

**Say to Cursor**:
```
Using contextcoding/CURSORRULES_GENERIC.md as reference, create a .cursorrules file in this project root. 
[If building an extension:] Also include extension-specific rules from CURSORRULES_EXTENSION_EXAMPLE.md.
```

Cursor will read the templates and create a customized `.cursorrules` file for your project.
