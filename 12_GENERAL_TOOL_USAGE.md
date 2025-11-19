# General Tool Usage & Workflow - JAUmemory Collection

This document contains non-project-specific memories about how to use the contextcoding workflow, learning system, agents, and tools. **Load these into JAUmemory as a collection** to have a reference guide for general workflow features.

## How to Load This Collection

**Say to Cursor**:
```
I want to load the general tool usage memories from 12_GENERAL_TOOL_USAGE.md into JAUmemory as a collection. 

Please:
1. Read 12_GENERAL_TOOL_USAGE.md
2. Create a collection named "General Tool Usage & Workflow"
3. Create each memory listed in the document
4. Add all memories to the collection
5. Confirm when complete
```

**Or manually**: Use the JAUmemory MCP tools to create each memory and add them to a collection.

---

## Memories to Load

### 1. Post-Resolution Learning Phase

**Content**:
```
Post-Resolution Learning Phase: Automatic learning system that runs after every bug fix. BLUE agent executes 4 steps: (1) Pattern Identification - searches codebase and JAUmemory for similar issues, (2) Prevention Strategy - creates prevention patterns and updates guardrails, (3) Automatic Detection - registers error signatures and code patterns for future auto-detection, (4) Knowledge Consolidation - consolidates related memories and updates agent learning. Creates Pattern Library, Blind-Spot Patterns, and Diagnostic Patterns collections automatically. No user prompt required - fully automatic.
```

**Tags**: `learning`, `workflow`, `meta-learning`, `pattern-detection`, `system-improvement`  
**Importance**: `0.9`  
**Context**: General tool usage - applies to all projects using the contextcoding workflow  
**Metadata**: 
- `type`: `workflow-feature`
- `automatic`: `true`
- `trigger`: `after-bug-fix`
- `agent`: `BLUE`
- `collections`: `["Pattern Library", "Blind-Spot Patterns", "Diagnostic Patterns"]`

---

### 2. META Agent (Meta-Learning Agent)

**Content**:
```
META Agent (Meta-Learning Agent): Oversees and improves the learning process itself. Automatically runs after every learning phase to evaluate effectiveness. Responsibilities: (1) Evaluate learning phase effectiveness, (2) Identify learning gaps, (3) Propose learning system improvements, (4) Monitor process for learning opportunities, (5) Intervene when learning is ineffective, (6) Create meta-learning insights. Can be invoked on-demand or periodically. Creates "Learning System Improvements" collection. Outputs Meta-Learning Report with effectiveness assessment, gaps identified, and improvements proposed.
```

**Tags**: `meta-learning`, `agent`, `learning-oversight`, `system-improvement`, `workflow`  
**Importance**: `0.9`  
**Context**: General tool usage - applies to all projects using the contextcoding workflow  
**Metadata**:
- `type`: `agent`
- `agentId`: `meta`
- `automatic`: `true`
- `trigger`: `after-learning-phase`
- `purpose`: `improve-learning-process`

---

### 3. Context Coding Repository (contextcoding)

**Content**:
```
Context Coding Repository (contextcoding): Starter kit for AI-assisted coding workflow. Contains 12 numbered documentation files covering: getting started, tooling overview, workflow guide, setup instructions, system prompt template, cursor rules (generic + extension-specific), default workflow manifest, JAUmemory quickstart, agent descriptions, and system diagram. Repository: https://github.com/shiftshapr/context-coding.git. Use for onboarding new collaborators and setting up new projects. All files are generic (not project-specific) with placeholders like [your-project-name].
```

**Tags**: `documentation`, `onboarding`, `starter-kit`, `workflow`, `tooling`  
**Importance**: `0.8`  
**Context**: General tool usage - repository for sharing workflow setup  
**Metadata**:
- `type`: `documentation`
- `repository`: `https://github.com/shiftshapr/context-coding.git`
- `fileCount`: `12`
- `purpose`: `onboarding-and-setup`

---

### 4. Pattern Library Collection

**Content**:
```
Pattern Library Collection: Automatic collection created by learning phase. Contains reusable patterns for automatic issue detection and prevention. Each pattern memory includes: error signature, code pattern, solution, prevention strategy, diagnostic script reference, and links to similar issues. Patterns are searchable by error signatures and code patterns. Used for automatic detection when similar errors appear. Agents can query patterns to surface solutions automatically. Part of the learning system that makes the system better at getting better.
```

**Tags**: `pattern`, `collection`, `auto-detection`, `learning`, `prevention`  
**Importance**: `0.85`  
**Context**: General tool usage - JAUmemory collection structure  
**Metadata**:
- `type`: `collection`
- `name`: `Pattern Library`
- `autoCreated`: `true`
- `purpose`: `pattern-storage-and-retrieval`

---

### 5. Workflow Execution Order

**Content**:
```
Workflow Execution Order: PM → SD → TEST → RED → WHITE → PURPLE → BLINDSPOT → BLUE → [LEARN] → [META] → DEVOPS → ETHICS. The [LEARN] phase is automatically executed by BLUE (not a separate agent). The [META] phase is automatically executed by META agent after learning phase. Both are mandatory and automatic - no user prompt required. Learning phase creates patterns, prevention strategies, and registers diagnostic patterns. META evaluates learning effectiveness and proposes improvements to the learning system itself.
```

**Tags**: `workflow`, `execution-order`, `agents`, `learning`, `meta-learning`  
**Importance**: `0.9`  
**Context**: General tool usage - workflow structure  
**Metadata**:
- `type`: `workflow`
- `agentCount`: `10`
- `phases`: `["LEARN", "META"]`
- `automatic`: `true`

---

### 6. 17 Core Agents

**Content**:
```
17 Core Agents: 10 workflow agents (PM, SD, TEST, RED, WHITE, PURPLE, BLINDSPOT, BLUE, DEVOPS, ETHICS) + 7 specialized agents (ORCH, CR, REFACTOR, DOC, EXP, TS, META). Workflow agents execute in order automatically. Specialized agents invoked as needed. META is the newest specialized agent for learning process oversight. All agents are stored in JAUmemory and can be queried with list_agents(). Agent memories can be linked to problems, and agents can create reflections for continuous improvement.
```

**Tags**: `agents`, `workflow`, `meta-learning`, `specialized-agents`  
**Importance**: `0.85`  
**Context**: General tool usage - agent structure  
**Metadata**:
- `type`: `agent-overview`
- `workflowAgents`: `10`
- `specializedAgents`: `7`
- `total`: `17`

---

### 7. System gets better at getting better

**Content**:
```
System gets better at getting better: Core principle of the learning system. Every bug fix triggers automatic learning phase that: (1) Identifies similar issues in codebase and JAUmemory, (2) Creates prevention patterns, (3) Registers diagnostic patterns for auto-detection, (4) Updates agent memories with learning. META agent then evaluates learning effectiveness and proposes improvements. This creates a feedback loop where the system continuously improves its ability to learn, prevent issues, and surface solutions automatically. No manual intervention required - fully automatic.
```

**Tags**: `meta-learning`, `system-improvement`, `feedback-loop`, `automatic`, `principle`  
**Importance**: `0.95`  
**Context**: General tool usage - core learning principle  
**Metadata**:
- `type`: `principle`
- `automatic`: `true`
- `feedbackLoop`: `true`
- `purpose`: `continuous-improvement`

---

### 8. Bike Rack Collection

**Content**:
```
Bike Rack Collection: A JAUmemory collection that contains tasks/issues you want to tackle. Check this collection when identifying new tasks. Query with list_collections() or get_collection(). Part of task identification workflow - always check Bike Rack before starting new work. Can be created manually or referenced in workflow guide. Helps organize backlog of tasks.
```

**Tags**: `collection`, `task-management`, `workflow`, `backlog`  
**Importance**: `0.7`  
**Context**: General tool usage - task organization  
**Metadata**:
- `type`: `collection`
- `name`: `Bike Rack`
- `purpose`: `task-backlog`
- `workflowStep`: `task-identification`

---

### 9. Diagnostic Script Requirements

**Content**:
```
Diagnostic Script Requirements: CRITICAL - All problems being worked on MUST have diagnostic scripts created to identify root causes. SD creates diagnostic scripts before coding. TEST runs diagnostics before and after implementation. Diagnostic scripts are registered as reusable patterns in Diagnostic Patterns collection. Scripts should check: data persistence, CSS/UI state, network requests, state management. Diagnostic results are attached to problem memory. Exception: time-sensitive issues where script isn't useful.
```

**Tags**: `diagnostic`, `root-cause`, `requirement`, `workflow`, `testing`  
**Importance**: `0.9`  
**Context**: General tool usage - diagnostic requirements  
**Metadata**:
- `type`: `requirement`
- `mandatory`: `true`
- `createdBy`: `SD`
- `executedBy`: `TEST`
- `exception`: `time-sensitive-issues`

---

### 10. Text Replacement Shortcut

**Content**:
```
Text Replacement Shortcut: Set up text expansion tool (Text Replacements on Mac, aText, AutoKey, etc.) with shortcut `;orch` that expands to full system prompt from 05_SYSTEM_PROMPT.md. Saves time since system prompt is used frequently. After expansion, replace [describe bug clearly] with actual task and [your-project-name] with project name. Can also add browser console logs if available. Part of workflow efficiency improvements.
```

**Tags**: `productivity`, `shortcut`, `system-prompt`, `workflow`  
**Importance**: `0.75`  
**Context**: General tool usage - productivity tip  
**Metadata**:
- `type`: `productivity-tip`
- `shortcut`: `;orch`
- `file`: `05_SYSTEM_PROMPT.md`
- `purpose`: `quick-access`

---

## Collection Details

**Collection Name**: `General Tool Usage & Workflow`  
**Description**: Non-project-specific memories about how to use the contextcoding workflow, learning system, agents, and tools. Reference guide for general workflow features.

**Total Memories**: 10

---

## Quick Import Script

If you want Cursor to automate the import, say:

```
Load all memories from 12_GENERAL_TOOL_USAGE.md into JAUmemory:

1. Create a collection named "General Tool Usage & Workflow" with description "Non-project-specific memories about how to use the contextcoding workflow, learning system, agents, and tools. Reference guide for general workflow features."

2. For each memory section (1-10), create a memory with:
   - Content: [the content from the section]
   - Tags: [the tags listed]
   - Importance: [the importance value]
   - Context: [the context listed]
   - Metadata: [the metadata object]

3. Add all 10 memories to the collection

4. Confirm when complete with the collection ID
```

---

## Why This Collection?

This collection provides:
- **Quick reference** for general workflow features
- **Consistency** across projects using the contextcoding workflow
- **Onboarding** for new collaborators
- **Documentation** of core principles and practices
- **Foundation** for project-specific memories

Load this collection into JAUmemory when setting up a new project or onboarding new team members to ensure everyone has access to the general workflow knowledge.


