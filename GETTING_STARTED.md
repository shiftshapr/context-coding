# Getting Started - Quick Start Guide

This guide helps you get the contextcoding repository and set up your environment. Choose the path that matches your experience level.

---

## For Beginners (New to GitHub)

### Step 1: Install Git (If You Don't Have It)

**On Mac**:
1. Open Terminal (search "Terminal" in Spotlight)
2. Type: `git --version`
3. If it says "command not found", install it:
   - Go to https://git-scm.com/download/mac
   - Download and install

**On Windows**:
1. Go to https://git-scm.com/download/win
2. Download and install Git for Windows
3. During installation, choose "Git from the command line and also from 3rd-party software"

**On Linux**:
```bash
# Ubuntu/Debian
sudo apt-get install git

# Fedora
sudo dnf install git
```

### Step 2: Get the Repository

**Option A: Download as ZIP (Easiest)**

1. Go to: https://github.com/shiftshapr/context-coding
2. Click the green **"Code"** button
3. Click **"Download ZIP"**
4. Extract the ZIP file to a folder (e.g., `Documents/contextcoding`)
5. Open that folder

**Option B: Use GitHub Desktop (Recommended for Beginners)**

1. Download GitHub Desktop: https://desktop.github.com/
2. Install and sign in with your GitHub account
3. Click **"File" → "Clone Repository"**
4. Go to the **"URL"** tab
5. Paste: `https://github.com/shiftshapr/context-coding.git`
6. Choose where to save it (e.g., `Documents/contextcoding`)
7. Click **"Clone"**

### Step 3: Open the Files

**Using a Text Editor**:
- Open the folder you downloaded/cloned
- Double-click any `.md` file to read it
- Start with `README.md` or `TOOLING_OVERVIEW.md`

**Using Cursor IDE** (Recommended):
1. Open Cursor IDE
2. Click **"File" → "Open Folder"**
3. Select the `contextcoding` folder you downloaded/cloned
4. You can now read and edit files in Cursor

### Step 4: Next Steps

Once you have the files:
1. Read `TOOLING_OVERVIEW.md` to understand the tools
2. Read `WORKFLOW_GUIDE.md` to learn the workflow
3. Follow `SETUP_AND_ONBOARDING.md` for detailed setup

---

## For Experienced GitHub Users

### Quick Clone

```bash
# Clone the repository
git clone https://github.com/shiftshapr/context-coding.git

# Navigate into the directory
cd context-coding

# View available files
ls -la
```

### Recommended Reading Order

```bash
# Read in this order:
1. TOOLING_OVERVIEW.md      # Understand all tools
2. WORKFLOW_GUIDE.md         # Complete workflow process
3. SETUP_AND_ONBOARDING.md   # Detailed setup instructions
4. SYSTEM_PROMPT.md          # Orchestration prompt template
5. CURSORRULES_GENERIC.md    # Universal rules
6. JAUMEMORY_CONTEXT_QUICKSTART.md  # Memory management
```

### Keeping the Repo Updated

```bash
# If you cloned it, pull latest changes:
cd context-coding
git pull origin main

# If you downloaded ZIP, just download a new ZIP when updates are available
```

### Forking (If You Want Your Own Copy)

```bash
# On GitHub website:
1. Go to https://github.com/shiftshapr/context-coding
2. Click "Fork" button (top right)
3. This creates your own copy

# Then clone your fork:
git clone https://github.com/YOUR-USERNAME/context-coding.git
cd context-coding
```

---

## What You'll Find in This Repo

- **TOOLING_OVERVIEW.md** - Complete guide to all tools (start here)
- **WORKFLOW_GUIDE.md** - Step-by-step workflow process
- **SETUP_AND_ONBOARDING.md** - Detailed setup instructions
- **SYSTEM_PROMPT.md** - The orchestration prompt template
- **CURSORRULES_GENERIC.md** - Universal project rules
- **CURSORRULES_EXTENSION_EXAMPLE.md** - Extension-specific rules
- **DEFAULT_WORKFLOW_MANIFEST.md** - 10-agent workflow definition
- **JAUMEMORY_CONTEXT_QUICKSTART.md** - Memory management guide
- **AGENT_DESCRIPTIONS.md** - Agent roles and responsibilities
- **SYSTEM_DIAGRAM_PROMPT.md** - Visual diagram generation prompt

---

## Quick Start Checklist

- [ ] Repository downloaded/cloned
- [ ] Files accessible (can open and read `.md` files)
- [ ] Read `TOOLING_OVERVIEW.md`
- [ ] Read `WORKFLOW_GUIDE.md`
- [ ] Ready to follow `SETUP_AND_ONBOARDING.md` for full setup

---

## Need Help?

**If you're stuck**:
1. Check `SETUP_AND_ONBOARDING.md` for detailed instructions
2. Ask Cursor: "Help me set up the contextcoding repository"
3. Review `TOOLING_OVERVIEW.md` for tool explanations

**Common Issues**:

**"Git command not found"**
- Install Git (see Step 1 for beginners)

**"Can't open .md files"**
- Use a text editor (VS Code, Cursor, Notepad++, etc.)
- Or use GitHub's web interface to read files

**"Don't know where to start"**
- Start with `TOOLING_OVERVIEW.md`
- Then read `WORKFLOW_GUIDE.md`
- Then follow `SETUP_AND_ONBOARDING.md`

---

## Repository URL

**GitHub**: https://github.com/shiftshapr/context-coding

**Clone URL**: `https://github.com/shiftshapr/context-coding.git`

