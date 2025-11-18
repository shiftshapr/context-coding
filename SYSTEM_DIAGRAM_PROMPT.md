# System Architecture Diagram - Image Generation Prompt

Use this prompt with DALL-E, Midjourney, Stable Diffusion, or similar image generation tools to create a visual system diagram.

## Image Generation Prompt

```
Create a professional system architecture diagram showing an AI coding orchestration workflow. The diagram should show:

CENTRAL: Cursor IDE (large box in center) with "Multi-Agent Orchestration" label

CONNECTED TO CURSOR (radiating outward):
1. System Prompt (top) - text bubble with "Orch, initialize..." 
2. .cursorrules (top-right) - policy document icon
3. JAUmemory (right) - database/cloud icon containing:
   - "47 Agents" label
   - "Memories/Collections" label
   - "Default Workflow" embedded inside showing "PM → SD → TEST → RED → WHITE → PURPLE → BLINDSPOT → BLUE → DEVOPS → ETHICS"
4. Browser Console (bottom-right) - DevTools window showing console/network tabs
5. Git Repository (bottom) - git branch icon with commit history
6. ESLint (bottom-left) - linting/checkmark icon
7. Text Replacement Tool (left) - keyboard shortcut icon with ";orch" label
8. Cursor Revert (left-center) - undo/rollback icon with "Manual AI Undo" label

DATA FLOW ARROWS:
- System Prompt → Cursor (thick arrow)
- .cursorrules → Cursor (enforcement arrow)
- Cursor ↔ JAUmemory (bidirectional, problem tracking, workflow recall)
- Browser Console → System Prompt (diagnostic data)
- Cursor → Git (commit arrow)
- Git → Cursor (revert/rollback arrow)
- Cursor → Cursor Revert (undo AI changes arrow)
- ESLint → Cursor (error feedback)
- Text Replacement → System Prompt (expansion)

STYLE:
- Clean, modern, technical diagram
- Blue/purple color scheme
- Icons for each component
- Clear labels
- Professional software architecture aesthetic
- White background
- Arrows showing data flow and dependencies
```

## Alternative: Mermaid Diagram (Text-Based)

If you prefer a text-based diagram that can be rendered in Markdown:

```mermaid
graph TB
    SP[System Prompt<br/>;orch shortcut] --> Cursor
    CR[.cursorrules<br/>Red-line Policies] --> Cursor
    
    subgraph JM[JAUmemory]
        Agents[47 Agents<br/>PM, SD, TEST, RED, etc.]
        Memories[Memories & Collections]
        WF[Default Workflow<br/>10-Agent Chain<br/>PM→SD→TEST→RED→WHITE→<br/>PURPLE→BLINDSPOT→BLUE→<br/>DEVOPS→ETHICS]
    end
    
    Cursor -->|Orchestrates| Agents
    Cursor -->|Recalls| WF
    Agents -->|Store| Memories
    Memories -->|Recall| Cursor
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

## Components to Include

1. **Cursor IDE** - Central hub
2. **System Prompt** - Orchestration trigger
3. **.cursorrules** - Policy enforcement
4. **JAUmemory** - Knowledge base containing:
   - 47 agents (PM, SD, TEST, RED, WHITE, PURPLE, BLINDSPOT, BLUE, DEVOPS, ETHICS, etc.)
   - Memories & Collections
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

