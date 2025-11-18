# Default Collaboration Workflow Manifest

## Overview
This manifest defines the standard agent collaboration workflow for all orchestrated tasks. All agents must follow this workflow and enforce blind-spot and red-line audits.

## Workflow Guardrails

1. **TypeScript ES Modules**: All new/updated code must use ES6 module syntax with TypeScript (no CommonJS, no implicit globals).
2. **Modular Architecture**: Prefer small, composable modules over monolithic files; refactors should extract shared utilities instead of duplicating logic.
3. **No Pre-Launch Backward Compatibility Paths**: Remove legacy fallbacks/duplicated fields during implementation. Exceptions require PM + BLUE sign-off and must be logged in JAUmemory.
4. **Duplication Checks**: Before writing new utilities/components, search for existing equivalents and extend them. Document the check in JAUmemory.
5. **Plan → Scaffold → Build**: Each task must capture planning notes, scaffolding artifacts, and the final build steps inside JAUmemory before coding progresses.
6. **Avoid Fallbacks**: Do not rely on `value || fallback` patterns that hide data issues. Fix the upstream source and document diagnostic evidence.
7. **Commit on Resolution**: After BLUE approval, produce a final commit referencing the JAUmemory problem ID and summarize verification steps.
8. **Unify Repeated Logic**: Look for opportunities to extract shared helpers/modules whenever similar code appears; log the reuse decision in JAUmemory.
9. **JAUmemory Logging**: Every phase update (problem, diagnostics, solution, verification, blind-spots, red-line status) must be logged with context, files, and owners.

## Parallel Orchestration Protocol

For time-consuming yet partitionable tasks (e.g., medium refactors, cleanup passes, diagnostic conversions):
- PM must evaluate whether work can be distributed. If yes, **ask the user to spin up 8–10 parallel Orch sessions**.
- Provide each Orch with:
  - Unique sub-objectives/files
  - Estimated runtime parity
  - Links to the shared JAUmemory problem + diagnostics
- BLUE must confirm that coordination overhead is addressed (shared standups, integration plan) before approving completion.

## Problem Tracking and Memory Management

All agents must follow this knowledge management process to ensure problems are tracked, solutions are documented, and knowledge is preserved across sessions.

### Problem Identification Phase
When a problem is identified:
1. **Check JAUmemory** for existing records of the same or similar problems
   - Search using relevant keywords, tags, and context
   - Review related memories for patterns or recurring issues
   
2. **If problem not found**, create a new memory with:
   - **Content**: Clear problem description
   - **Context**: Project name, component, affected systems
   - **Tags**: Categorization tags (e.g., "bug", "frontend", "database", "api")
   - **Importance**: Severity score (0.0-1.0)
   - **Metadata**: 
     - Status: "identified"
     - Root cause analysis (if known)
     - Impact assessment
     - Related components/files

### Solution Proposal Phase
When proposing solutions:
1. **Update the memory** with:
   - **Content**: Updated with proposed solution(s)
   - **Metadata**:
     - Status: "proposed"
     - Proposed solution(s) description
     - Implementation plan
     - Risk assessment
     - Dependencies
     - Estimated effort

2. **Link related memories** if the problem relates to other issues

### Solution Implementation Phase
During implementation:
1. **Update the memory** with:
   - **Content**: Updated with implementation details
   - **Metadata**:
     - Status: "implemented"
     - Code changes made
     - Files modified
     - Testing approach
     - Implementation notes

### Verification Phase
After implementation:
1. **Update the memory** with:
   - **Content**: Updated with verification results
   - **Metadata**:
     - Status: "solved" or "failed"
     - Verification results
     - Test outcomes
     - Confirmation of fix
     - Lessons learned
     - Related memories/agents

2. **Link to related memories** for better knowledge graph

### Knowledge Consolidation
Periodically (at end of tasks or weekly):
1. **Consolidate similar problems** into insights
   - Use `consolidate_collection()` to group related memories
   - Create summary insights from patterns
   - Archive original memories if consolidated

2. **Update agent memories** with lessons learned
   - Link solved problems to relevant agents
   - Update agent knowledge base
   - Share insights across agents

### Memory Management Best Practices
- **Always check first**: Before creating new memories, search for existing ones
- **Be specific**: Include enough context for future recall
- **Use tags**: Consistent tagging improves searchability
- **Link related**: Connect related problems and solutions
- **Update status**: Keep memory status current throughout the workflow
- **Consolidate regularly**: Group similar issues to identify patterns

### Integration with Agent Workflow
- **PM**: Responsible for initial problem identification and memory creation
- **SD**: Updates memory with proposed solutions
- **TEST**: Updates memory with test results
- **All Agents**: Update memory when identifying new problems or solutions
- **BLUE**: Finalizes memory status and triggers consolidation

## Diagnostic Script Requirements

**CRITICAL**: All problems being worked on MUST have diagnostic scripts created to identify root causes, regardless of whether a solution is being provided (except when a script is not useful, e.g., time-sensitive issues).

### Diagnostic Script Framework
A comprehensive diagnostic framework is available at `/presence/utils/ROOT_CAUSE_DIAGNOSTIC_FRAMEWORK.js` that provides:
- Standardized diagnostic structure
- Multiple diagnostic types (data persistence, CSS, network, state)
- Automatic result collection and reporting
- Easy registration of new diagnostics

### When to Create Diagnostic Scripts
1. **Always**: When working on any bug or issue
2. **Always**: Before implementing a solution (to understand root cause)
3. **Always**: After implementing a solution (to verify the fix)
4. **Exception**: When a script is not useful (e.g., time-sensitive issues, user-reported visual issues that require manual inspection)

### Diagnostic Script Requirements

#### For Data Persistence Issues
- Check all data sources (Chrome storage, UserPreferencesManager, window.currentUser, database)
- Verify consistency across sources
- Test save operations and verify persistence
- Log all values from each source
- Identify where data is missing or inconsistent

#### For CSS/UI Issues
- Log computed CSS values for affected elements
- Check data attributes (e.g., `data-theme`)
- Verify element existence and visibility
- Log bounding rectangles and layout properties
- Check for CSS conflicts or overrides
- **Ask user to check**: Browser DevTools (Elements, Console, Network tabs)

#### For Network/API Issues
- Log all network requests (URL, duration, status, response)
- Check for failed requests
- Verify request/response payloads
- Check authentication headers
- Identify timing issues

#### For State Management Issues
- Log current state of relevant managers
- Check initialization status
- Verify queue sizes (batch, retry)
- Check online/offline status
- Log metrics and error counts

### Diagnostic Script Structure
```javascript
diagnosticFramework.register('issue-name', async () => {
  const results = {
    timestamp: new Date().toISOString(),
    // Diagnostic checks here
  };
  
  // Perform checks
  // Log findings
  // Return structured results
  
  return results;
}, 'Description of what this diagnostic checks');
```

### Diagnostic Script Execution
- **Automatic**: Scripts can be registered to run automatically
- **Manual**: Call `diagnoseIssue('issue-name')` for specific diagnostics
- **Comprehensive**: Call `diagnoseAll()` to run all diagnostics
- **Results**: Access via `getDiagnosticResults()`

### User Interaction Requests
Diagnostic scripts should request user assistance when needed:
- **Visual inspection**: "Please check the interface - does [element] appear correctly?"
- **Console check**: "Please check the browser console for errors"
- **Network check**: "Please check the Network tab - are there any failed requests?"
- **Elements check**: "Please inspect [element] in DevTools - what are its computed styles?"

### Integration with Agent Workflow
- **PM**: Identifies need for diagnostic scripts during problem analysis
- **SD**: Creates diagnostic scripts as part of solution design
- **TEST**: Uses diagnostic scripts to verify fixes
- **All Agents**: Can request diagnostic scripts be created for their domain
- **BLUE**: Verifies diagnostic scripts were created and executed

## Agent Roles and Responsibilities

### 1. PM (Project Manager)
**Role**: Problem analysis, requirements validation, scope definition
**Responsibilities**:
- Analyze the problem statement
- **Check JAUmemory for existing problems** and related solutions
- **Create/update memory** for identified problems (if not found)
- **Identify need for diagnostic scripts** to understand root causes
- Validate requirements completeness
- Identify dependencies and constraints
- Define success criteria
- Document current state vs desired state
- Escalate red-line violations
- **Update memory** with problem analysis and initial root cause assessment
- **Request diagnostic scripts** be created for the problem domain

**Output**: Problem Analysis Report

### 2. SD (Solution Designer)
**Role**: Architecture and solution design
**Responsibilities**:
- **Review problem memory** from PM phase
- **Create diagnostic scripts** to identify root causes before designing solution
- Design solution architecture
- Define data flows and interfaces
- Specify implementation approach
- Identify technical risks
- Create implementation plan
- Ensure alignment with existing systems
- **Update memory** with proposed solution(s) and implementation plan
- **Ensure diagnostic scripts cover** all aspects of the problem domain

**Output**: Solution Design Document

### 3. TEST (Test Engineer)
**Role**: Test planning and verification
**Responsibilities**:
- Create comprehensive test plan
- Define test cases and scenarios
- Identify edge cases
- Plan integration testing
- Define acceptance criteria
- **Use diagnostic scripts** to verify fixes and identify remaining issues
- **Create additional diagnostic scripts** for test scenarios
- Execute tests and report results
- **Run diagnostic scripts** before and after fixes to verify changes

**Output**: Test Plan and Test Results

### 4. RED (Red-Line Auditor)
**Role**: Critical constraint enforcement
**Responsibilities**:
- Audit against red-line constraints
- Identify violations
- Escalate critical issues
- Verify compliance with policies
- Check for breaking changes
- Validate data integrity requirements

**Output**: Red-Line Audit Report

### 5. WHITE (White-Hat Security)
**Role**: Security review
**Responsibilities**:
- Security vulnerability assessment
- Authentication/authorization review
- Data protection verification
- Input validation checks
- Secure communication review
- Security best practices compliance

**Output**: Security Review Report

### 6. PURPLE (Purple-Team Testing)
**Role**: Adversarial testing
**Responsibilities**:
- Simulate attack scenarios
- Test error handling
- Test edge cases and boundary conditions
- Test failure modes
- Test resilience and recovery
- Test under adverse conditions

**Output**: Adversarial Test Results

### 7. BLINDSPOT (Blind-Spot Analyst)
**Role**: Identify overlooked issues
**Responsibilities**:
- Identify assumptions
- Find edge cases not covered
- Identify integration points
- Check for race conditions
- Verify error handling completeness
- Identify performance implications

**Output**: Blind-Spot Analysis Report

### 8. BLUE (Blue-Hat Final Review)
**Role**: Final quality gate
**Responsibilities**:
- Review all previous outputs
- Verify completeness
- Confirm all audits passed
- Final approval for deployment
- Sign-off on implementation
- Document final state
- **Update problem memory** with final status ("solved" or "failed")
- **Trigger memory consolidation** for related problems
- **Link solved problems** to relevant agent memories

**Output**: Final Approval Report

### 9. DEVOPS (DevOps Engineer)
**Role**: Deployment and operations
**Responsibilities**:
- Deployment planning
- Infrastructure requirements
- Monitoring and alerting setup
- Rollback procedures
- Performance considerations
- Operational runbooks

**Output**: Deployment Plan

### 10. ETHICS (Ethics Reviewer)
**Role**: Ethical considerations
**Responsibilities**:
- Privacy impact assessment
- User consent verification
- Data handling compliance
- Accessibility review
- Fairness and bias checks
- Ethical use verification

**Output**: Ethics Review Report

## Workflow Execution Order

```
PM → SD → TEST → RED → WHITE → PURPLE → BLINDSPOT → BLUE → DEVOPS → ETHICS
```

## Blind-Spot Audit Checklist
- [ ] Are all edge cases covered?
- [ ] Are all error scenarios handled?
- [ ] Are race conditions considered?
- [ ] Are integration points verified?
- [ ] Are performance implications assessed?
- [ ] Are security implications considered?
- [ ] Are accessibility requirements met?
- [ ] Are user experience implications considered?

## Red-Line Audit Checklist
- [ ] No breaking changes to existing APIs
- [ ] Data integrity maintained
- [ ] Security policies followed
- [ ] Privacy requirements met
- [ ] Performance thresholds maintained
- [ ] Backward compatibility preserved
- [ ] Critical constraints not violated

## Escalation Criteria
Escalate to PM if:
- Red-line violations found
- Critical security issues identified
- Breaking changes required
- Scope expansion needed
- Resource constraints identified

## Reporting Requirements
Each agent must produce:
1. Status: PASSED | FAILED | WARNINGS
2. Findings: List of issues found
3. Recommendations: Suggested fixes
4. Risk Assessment: Risk level and mitigation
5. **Memory Updates**: Any problems identified must be recorded in JAUmemory with appropriate status updates
6. **Diagnostic Scripts**: Diagnostic scripts created and executed (if applicable)
7. **Diagnostic Results**: Summary of diagnostic findings and root cause analysis

## Final Approval
All agents must PASS before BLUE can approve. Any FAILED agent requires fixes and re-audit.

