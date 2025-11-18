# Getting Started - Quick Start Guide

This guide helps you get the contextcoding repository and set up your environment. Choose the path that matches your experience level.

---

## For Beginners (New to GitHub)

### Step 1: Review Files on GitHub First

**Before downloading anything**, you can read all the files directly on GitHub:

1. Go to: https://github.com/shiftshapr/context-coding
2. Click on any `.md` file to read it
3. Start with `README.md` or `TOOLING_OVERVIEW.md`
4. This helps you understand what you're getting

**Why clone?** You need to clone (not just download) so that Cursor IDE can access these files to set up your AI coding system. Cursor needs the files on your local machine to reference them.

### Step 2: Install Git (Required for Cloning)

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

### Step 3: Clone the Repository (Required for Cursor)

**You must clone (not just download)** so Cursor can access the files.

**Option A: Use GitHub Desktop (Easiest for Beginners)**

1. Download GitHub Desktop: https://desktop.github.com/
2. Install and sign in with your GitHub account (or create one)
3. Click **"File" → "Clone Repository"**
4. Go to the **"URL"** tab
5. Paste: `https://github.com/shiftshapr/context-coding.git`
6. **Choose your coding/projects folder** (e.g., `Documents/Projects` or `~/code`)
7. Click **"Clone"**
8. The folder will be saved as `context-coding` in the location you chose

**Option B: Use Terminal/Command Line**

1. Open Terminal (Mac/Linux) or Git Bash (Windows)
2. Navigate to where you keep your coding projects:
   ```bash
   cd ~/Documents/Projects
   # or wherever you keep your code
   ```
3. Clone the repository:
   ```bash
   git clone https://github.com/shiftshapr/context-coding.git
   ```
4. Navigate into it:
   ```bash
   cd context-coding
   ```

### Step 4: Open in Cursor IDE

**This is why you cloned it** - so Cursor can use these files:

1. Open Cursor IDE
2. Click **"File" → "Open Folder"**
3. Navigate to and select the `context-coding` folder you just cloned
4. Cursor can now:
   - Read the files to set up your AI coding system
   - Reference `.cursorrules` templates
   - Use the system prompt templates
   - Access workflow definitions

### Step 5: Next Steps

Once you've cloned and opened in Cursor:
1. Read `TOOLING_OVERVIEW.md` to understand the tools
2. Read `WORKFLOW_GUIDE.md` to learn the workflow
3. Follow `SETUP_AND_ONBOARDING.md` for detailed setup
4. Cursor will use these files to configure your AI coding system

---

## For Experienced GitHub Users

### Quick Clone

**Clone to your coding/projects directory** so Cursor can access it:

```bash
# Navigate to your projects directory
cd ~/code  # or wherever you keep projects

# Clone the repository
git clone https://github.com/shiftshapr/context-coding.git

# Navigate into the directory
cd context-coding

# View available files
ls -la
```

**Then open in Cursor**:
- `File → Open Folder` → select `context-coding`
- Cursor will use these files to set up your AI coding system

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

- [ ] Reviewed files on GitHub (optional, but helpful)
- [ ] Git installed
- [ ] Repository cloned to your coding/projects directory
- [ ] Opened `context-coding` folder in Cursor IDE
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
- Open the folder in Cursor IDE (File → Open Folder)
- Or use GitHub's web interface to read files
- Cursor needs the files cloned locally to use them for AI coding setup

**"Don't know where to start"**
- Start with `TOOLING_OVERVIEW.md`
- Then read `WORKFLOW_GUIDE.md`
- Then follow `SETUP_AND_ONBOARDING.md`

---

## Repository URL

**GitHub**: https://github.com/shiftshapr/context-coding

**Clone URL**: `https://github.com/shiftshapr/context-coding.git`

