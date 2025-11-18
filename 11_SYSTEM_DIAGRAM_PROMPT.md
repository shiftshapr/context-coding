# System Architecture Diagram

```mermaid
graph TB
    SP[System Prompt<br/>;orch shortcut] --> Cursor
    CR[.cursorrules<br/>Red-line Policies] --> Cursor
    
    subgraph JM[JAUmemory]
        Agents[17 Core Agents<br/>PM, SD, TEST, RED, WHITE,<br/>PURPLE, BLINDSPOT, BLUE,<br/>DEVOPS, ETHICS, ORCH,<br/>CR, REFACTOR, DOC, EXP, TS, META]
        Memories[Memories & Collections]
        Prefs[Preferences & Policies<br/>Project Settings]
        WF[Default Workflow<br/>10-Agent Chain<br/>PM→SD→TEST→RED→WHITE→<br/>PURPLE→BLINDSPOT→BLUE→<br/>DEVOPS→ETHICS]
    end
    
    Cursor -->|Orchestrates| Agents
    Cursor -->|Recalls| WF
    Cursor -->|Recalls| Prefs
    Agents -->|Store| Memories
    Memories -->|Recall| Cursor
    Prefs -->|Project Context| Cursor
    WF -->|Execution Order| Cursor
    
    BC[Browser Console<br/>DevTools] -->|Logs/Errors| SP
    SP -->|Includes| BC
    
    Cursor -->|Lints| ESLint[ESLint<br/>Code Quality]
    ESLint -->|Feedback| Cursor
    
    Cursor -->|Commits| Git[Git Repository<br/>Version Control]
    Git -->|Revert/Rollback| Cursor
    
    Cursor -->|Undo AI Changes| Revert[Cursor Revert<br/>Manual AI Undo]
    
    TR[Text Replacement<br/>;orch expansion] -->|Loads| SP
    
    style Cursor fill:#4A90E2,stroke:#2E5C8A,stroke-width:3px,color:#fff
    style JM fill:#9B59B6,stroke:#6C3483,stroke-width:2px,color:#fff
    style Agents fill:#E74C3C,stroke:#C0392B,stroke-width:2px,color:#fff
    style SP fill:#27AE60,stroke:#1E8449,stroke-width:2px,color:#fff
    style Revert fill:#E67E22,stroke:#D35400,stroke-width:2px,color:#fff
```

## Components

1. **Cursor IDE** - Central hub
2. **System Prompt** - Orchestration trigger
3. **.cursorrules** - Policy enforcement
4. **JAUmemory** - Knowledge base containing:
   - 17 core agents:
     - **Workflow agents** (10): PM, SD, TEST, RED, WHITE, PURPLE, BLINDSPOT, BLUE, DEVOPS, ETHICS
     - **Specialized agents** (7): ORCH (orchestration), CR (code research), REFACTOR (optimization), DOC (documentation), EXP (UX/UI), TS (TypeScript), META (meta-learning/learning oversight)
   - Memories & Collections
   - Preferences & Policies (project-specific settings recalled at orchestration start)
   - Default Workflow (10-agent execution chain stored in JAUmemory)
5. **Browser Console** - Runtime diagnostics
6. **Git** - Version control (with revert/rollback capability)
7. **Cursor Revert** - Manual AI undo/rollback feature
8. **ESLint** - Code quality
9. **Text Replacement** - Productivity shortcut

## Visual Style Notes

- Use consistent iconography
- Show bidirectional data flow where applicable
- Highlight Cursor as the central orchestrator
- Use color coding: Blue (Cursor), Purple (JAUmemory), Red (Agents), Green (System Prompt), Orange (Cursor Revert)
- Show Default Workflow as embedded within JAUmemory, not as separate component
- Include labels for clarity
- Show both setup phase (configuration) and runtime phase (execution)

