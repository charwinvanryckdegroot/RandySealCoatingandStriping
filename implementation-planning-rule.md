# Implementation Planning Rule

## Core Directive
Before implementing ANY new feature, function, or system component, you MUST complete a comprehensive implementation plan following the structure below. This planning phase is mandatory and ensures nothing is overlooked.

## Planning Structure

### 1. REQUIREMENT ANALYSIS
- **Primary Goal**: What is the core objective of this implementation?
- **User Stories**: Who will use this and how? What problems does it solve?
- **Success Criteria**: How will we measure if this implementation is successful?
- **Constraints**: What limitations exist (technical, time, resources, compatibility)?
- **Non-functional Requirements**: Performance, security, scalability, accessibility needs?

### 2. TECHNICAL DISCOVERY
- **Existing Code Analysis**: 
  - What current code will this interact with?
  - What patterns/conventions are already established?
  - What can be reused vs. what needs to be built new?
- **Dependencies**: 
  - What external libraries/APIs are needed?
  - Version compatibility concerns?
  - License restrictions?
- **Technology Stack Decisions**: 
  - Best tools/frameworks for this specific task?
  - Justification for each choice?

### 3. ARCHITECTURE DESIGN
- **High-Level Design**: 
  - Component/module structure
  - Data flow diagram
  - System boundaries and interfaces
- **Detailed Design**:
  - Class/function signatures
  - Data structures and schemas
  - API contracts (if applicable)
  - Database schema changes (if applicable)
- **Integration Points**: 
  - How does this fit into the existing architecture?
  - What systems will this need to communicate with?
  - What protocols/formats for communication?

### 4. IMPLEMENTATION BREAKDOWN
- **Task Decomposition**: 
  - Break into smallest implementable units
  - Identify dependencies between tasks
  - Estimate complexity for each task
- **Implementation Order**: 
  - What must be built first?
  - What can be built in parallel?
  - Critical path identification
- **File Structure**: 
  - What new files need to be created?
  - What existing files need modification?
  - Folder organization strategy

### 5. DATA & STATE MANAGEMENT
- **Data Requirements**: 
  - What data needs to be stored/retrieved?
  - Data validation rules
  - Data transformation needs
- **State Management**: 
  - Local vs. global state decisions
  - State persistence requirements
  - Caching strategy
- **Data Security**: 
  - Sensitive data identification
  - Encryption needs
  - Access control requirements

### 6. ERROR HANDLING & EDGE CASES
- **Failure Scenarios**: 
  - What can go wrong at each step?
  - Network failures, data corruption, race conditions
  - User input edge cases
- **Error Recovery**: 
  - Graceful degradation strategies
  - Rollback mechanisms
  - User feedback for errors
- **Logging & Monitoring**: 
  - What needs to be logged?
  - Performance metrics to track
  - Alerting thresholds

### 7. TESTING STRATEGY
- **Unit Tests**: 
  - Critical functions to test
  - Test data requirements
  - Mock/stub needs
- **Integration Tests**: 
  - Inter-component testing needs
  - API contract testing
  - End-to-end scenarios
- **Performance Tests**: 
  - Load testing requirements
  - Performance benchmarks
  - Optimization targets
- **User Acceptance Criteria**: 
  - Manual testing scenarios
  - Beta testing plan

### 8. SECURITY CONSIDERATIONS
- **Authentication/Authorization**: 
  - Who can access this feature?
  - Permission levels required
  - Token/session management
- **Input Validation**: 
  - All user inputs identified
  - Validation rules for each
  - Sanitization requirements
- **Security Vulnerabilities**: 
  - OWASP considerations
  - SQL injection, XSS, CSRF prevention
  - Rate limiting needs

### 9. PERFORMANCE & SCALABILITY
- **Performance Requirements**: 
  - Response time targets
  - Throughput requirements
  - Resource usage limits
- **Optimization Opportunities**: 
  - Caching strategies
  - Query optimization
  - Lazy loading possibilities
- **Scalability Planning**: 
  - Horizontal vs vertical scaling
  - Bottleneck identification
  - Future growth accommodation

### 10. USER EXPERIENCE
- **UI/UX Requirements**: 
  - User interface mockups/wireframes
  - Interaction patterns
  - Responsive design needs
- **Accessibility**: 
  - WCAG compliance needs
  - Screen reader compatibility
  - Keyboard navigation
- **User Feedback**: 
  - Loading states
  - Success confirmations
  - Progress indicators

### 11. DEPLOYMENT & ROLLOUT
- **Deployment Strategy**: 
  - Blue-green, canary, or direct?
  - Rollback plan
  - Database migration strategy
- **Configuration Management**: 
  - Environment variables needed
  - Feature flags
  - Configuration validation
- **Documentation Updates**: 
  - API documentation
  - User guides
  - Internal wiki/readme updates

### 12. MAINTENANCE & MONITORING
- **Monitoring Setup**: 
  - Health checks
  - Performance dashboards
  - Error tracking
- **Maintenance Plan**: 
  - Known technical debt
  - Future enhancement opportunities
  - Deprecation timeline (if replacing existing functionality)
- **Support Considerations**: 
  - Common issues anticipated
  - Troubleshooting guide
  - Support team training needs

## Implementation Plan Output Format

After analyzing all sections above, provide a structured implementation plan:

```markdown
## Implementation Plan: [Feature Name]

### Executive Summary
[2-3 sentence overview of what will be built and why]

### Prerequisites
- [ ] Dependency 1
- [ ] Dependency 2
- [ ] Setup requirement

### Implementation Phases

#### Phase 1: [Foundation/Setup]
**Duration**: X days
**Tasks**:
1. Task with specific acceptance criteria
2. Task with specific acceptance criteria

#### Phase 2: [Core Implementation]
**Duration**: X days
**Tasks**:
1. Task with specific acceptance criteria
2. Task with specific acceptance criteria

#### Phase 3: [Integration & Testing]
**Duration**: X days
**Tasks**:
1. Task with specific acceptance criteria
2. Task with specific acceptance criteria

### Risk Mitigation
- **Risk 1**: [Description] → **Mitigation**: [Strategy]
- **Risk 2**: [Description] → **Mitigation**: [Strategy]

### Definition of Done
- [ ] All unit tests passing
- [ ] Integration tests complete
- [ ] Documentation updated
- [ ] Code reviewed and approved
- [ ] Performance benchmarks met
- [ ] Security scan passed
- [ ] Deployed to staging
- [ ] User acceptance testing complete
```

## Usage Instructions
1. When a new feature/implementation is requested, STOP and run through this planning process
2. Ask clarifying questions if any section cannot be adequately addressed
3. Present the implementation plan for review before beginning any coding
4. Use the plan as a checklist during implementation
5. Update the plan if significant changes occur during implementation

## Key Principles
- **No assumptions**: If something is unclear, ask
- **Think holistically**: Consider the entire system, not just the immediate code
- **Plan for failure**: Every system fails; plan how yours will fail gracefully
- **Future-proof reasonably**: Don't over-engineer, but consider obvious future needs
- **Document decisions**: Your future self (and teammates) will thank you