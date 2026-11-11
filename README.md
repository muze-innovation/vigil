# VIGIL

> Verification of Intended Guidelines through Incremental Lifecycle analysis

The Git Diff Analyser

# What's VIGIL

A software development tool of Muze's Toolbelt to help review the code to ensure certain specific criteria is met on regular basis. Basically a code review with specific purpose.

## Example usecase: auto-logout

Consider an application with an existing Auto Logout feature.

The Software Architecture team wants to ensure that Auto Logout can only be triggered through three approved execution paths.

### Concern Definition

Concern: Auto Logout
Active

Expectation

Auto Logout must only be triggered through the following three approved paths:
1. Session expiration
2. Explicit user logout due to security policy
3. Token validation failure
Constraint

No additional Auto Logout execution paths should be introduced without architectural review.

Sources
- Application source repository
- Authentication architecture documentation
- Existing logout implementation references

### Initial analysis

VIGIL analyzes the existing codebase and identifies three known execution paths.

- Security policy → Auto Logout (ALLOWED)
- Session expiration, refresh failure → Auto Logout (NOT ALLOWED)
- Token validation failure, network timeout, etc → Auto Logout (NOT ALLOWED)

### In Subsequent monitoring

A developer introduces a new code path that the daily batch vigil monitoring found. Based on Git Diffs (from previous scans)

> New finding
> 4th execution paths detected!
> Evidence provided by VIGIL
> - Source file and relevant code location
> - Execution path leading to Auto Logout

The scan result sent to related stakeholders

# Core Concept

VIGIL revolves around four key concepts.

Concept|Description
--|--
Concern|A specific architectural expectation, business rule, or implementation constraint that must be monitored.
Evidence|Supporting information that helps VIGIL understand and validate a concern, such as documentation, code references, diagrams, or examples.
Repository|One or more source code repositories and specific branches associated with a concern.
Finding|An observed implementation behavior, deviation, or potential violation identified by VIGIL.

# How it works

1. Define Concerns - Developers define architectural concerns, expected behaviors, constraints, and acceptable implementation paths.
1. Provide Evidence & Sources - Attach relevant documentation, code references, examples, and repository/branch information.
1. Initial Analysis - VIGIL analyzes the current source code to understand the implementation, identify relevant code paths, and establish an initial baseline.
1. Generate Initial Report - VIGIL produces a report describing its findings, observed behaviors, known paths, and potential discrepancies for developer or architect review.
1. Continuous Monitoring - VIGIL periodically pulls the latest source code from configured branches and re-evaluates the defined concerns.
1. Detect & Notify - When new or unexpected implementation paths are discovered, VIGIL generates findings with supporting evidence and notifies the responsible stakeholders.

# Expected capabilities

The initial product should focus on:

- Concern Management: Create, update, and manage architectural concerns.
- Evidence Management: Associate documentation, code references, and supporting materials with concerns.
- Repository Integration: Connect repositories and monitor specific branches.
- AI Code Understanding: Analyze source code semantically rather than relying exclusively on textual Git diffs.
- Baseline Generation: Establish the initial understanding of existing implementations.
- Continuous Analysis: Periodically re-analyze the latest source code.
- Change Detection: Identify new code paths, unexpected behavior, and deviations from established expectations.
- Evidence-based Reporting: Provide traceable findings with relevant source code references.
- Notifications: Alert responsible stakeholders when significant deviations are detected.
