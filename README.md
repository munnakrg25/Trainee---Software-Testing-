# Software Tester (QA) Assessment — Task Management Application

## Assessment Overview

This repository contains my submission for the **Software Tester (QA) Assessment** issued by VirtuBox Infotech Private Limited. The assessment required designing test scenarios, detailed test cases, and a static (non-execution-based) bug/risk analysis for a **Task Management Application** that is close to production release and has no existing test documentation.

This submission demonstrates a structured, professional QA approach: how requirements were interpreted, how test coverage was planned, and how risks were identified through analysis rather than execution.

## Application Under Assessment

**Task Management Application** with the following stated features:

- User Registration & Login
- Logged-in users can:
  - Create a task
  - View task list
  - Edit a task
  - Delete a task
- Tasks are stored in a database and displayed in a list

No other features are assumed or tested beyond what is described above.

## Testing Objectives

- Validate that Registration and Login work correctly and securely for genuine users.
- Validate that Task CRUD (Create, Read/View, Update, Delete) operations behave correctly and preserve data integrity.
- Validate input handling and error handling across the application, including invalid, missing, and boundary input.
- Identify authentication and authorization gaps, since the application handles per-user data.
- Identify likely risk areas before execution, to help prioritize testing effort.

## Application Scope

**In scope:**
- Registration flow
- Login flow
- Task Create, View/List, Edit, Delete
- Input validation and error handling across the above flows

**Out of scope (not mentioned in the assessment, therefore not assumed):**
- Password reset / forgot password flow
- Task sharing, collaboration, or notifications
- Third-party integrations
- Mobile-specific or performance/load testing (only noted as a risk area, not executed)

## Features Under Test

| Feature Area        | Description |
|----------------------|-------------|
| Registration          | New user sign-up with name, email, and password |
| Login                 | Authentication using registered email and password |
| Task Create            | Adding a new task to the logged-in user's list |
| Task View/List          | Viewing the list of tasks belonging to the logged-in user |
| Task Edit               | Updating an existing task's details |
| Task Delete              | Removing an existing task |
| Input Validation           | Field-level validation across all forms |
| Error Handling               | Application behavior under failure/edge conditions |

## Test Coverage

The `Test-Cases.xlsx` workbook contains **53 test cases** across all 8 feature areas, covering:

- **Positive test cases** — expected, valid usage flows
- **Negative test cases** — invalid input, missing data, unauthorized access attempts
- **Edge cases** — unusual but plausible real-world conditions (session expiry, concurrent edits, script injection, network failure)
- **Boundary cases** — values at or beyond defined field/data limits
- **Authentication checks** — valid/invalid credentials, brute-force protection, session handling
- **Authorization checks** — ensuring users cannot access or modify another user's data
- **Data persistence checks** — verifying changes are correctly saved, reflected, and survive refresh

See the **Summary** sheet inside `Test-Cases.xlsx` for a breakdown of test case counts by module, type, and priority.

## Testing Approach

1. **Requirement analysis** — Reviewed the assessment document to identify all explicitly stated features and constraints (no test documentation exists, application is close to production).
2. **Test scenario identification** — Derived high-level scenarios for each feature area (Registration, Login, Task CRUD, Validation).
3. **Test case design** — Converted scenarios into detailed, reproducible test cases using a consistent format (ID, Precondition, Steps, Test Data, Expected Result, Type, Priority).
4. **Static risk analysis** — Reviewed the described functionality (without executing the application) to identify likely defect-prone areas, focusing on security, data integrity, and error handling — common risk areas in CRUD-based, multi-user applications.
5. **Prioritization** — Assigned priority (High/Medium/Low) to each test case based on business impact and risk, to guide execution order under time constraints.

## Test Case Categories

- Functional Testing (Registration, Login, Task CRUD)
- Positive Testing
- Negative Testing
- Edge Case Testing
- Boundary Testing
- Input Validation Testing
- Error Handling Testing
- Authentication Testing
- Authorization Testing
- Data Integrity / Data Persistence Testing
- Basic Security Testing (XSS/SQL injection input handling, at a black-box level)

## Testing Priorities

If execution were time-boxed, the recommended order would be:

1. **High priority:** Security-related and authorization test cases (unauthorized data access, SQL/script injection handling, invalid session/token handling) — these carry the highest business and data-privacy risk.
2. **High priority:** Core CRUD happy-path test cases (Register, Login, Create/View/Edit/Delete a task) — these validate the application's primary purpose.
3. **Medium priority:** Negative and validation test cases (invalid input, missing fields, mismatched passwords).
4. **Low/Medium priority:** Edge and boundary cases (concurrency, large data volume, whitespace-only input, casing).

## Security and Authorization Considerations

Because this application stores **per-user data** (tasks tied to a specific account), authentication and authorization were treated as first-class concerns rather than an afterthought:

- Verifying that one user cannot view, edit, or delete another user's tasks (broken access control is a common and high-severity risk in multi-user CRUD apps).
- Verifying that login failures do not reveal whether a specific email is registered (prevents user enumeration).
- Verifying that repeated failed login attempts are rate-limited or locked out (prevents brute-force attacks).
- Verifying that client-side validation is **not** the only line of defense — server-side validation must independently reject bad or malicious input.
- Verifying that script/SQL-like input is safely handled (escaped/sanitized) rather than executed or causing a database error.

These are treated as **test cases and hypothetical risk areas**, not confirmed vulnerabilities, since the application was not executed.

## Testing Flow

```
Requirement Review
        |
Test Scenario Identification
        |
Detailed Test Case Design (Test-Cases.xlsx)
        |
Static Bug/Risk Analysis (Potential-Bugs.md)
        |
Prioritization & Reporting (this README)
```

## Entry Criteria

- Assessment document/requirements are available and understood.
- Application feature list is finalized (Registration, Login, Task CRUD, as stated).
- Test case template/format is defined.

## Exit Criteria

- Test cases designed for all in-scope modules, covering positive, negative, edge, and boundary conditions.
- At least 8–10 potential risk areas documented with severity and impact.
- All deliverables (README, Test-Cases.xlsx, Potential-Bugs.md) are consistent with each other and with the original assessment document.

*(Note: Since the application was not executed as part of this assessment, "exit criteria" here refers to completeness of test design and analysis, not pass/fail execution results.)*

## Assumptions

Since the assessment states there is **no existing test documentation**, the following reasonable assumptions were made strictly within the described scope:

- Registration requires Name, Email, and Password (with a Confirm Password step assumed as standard practice).
- Login uses Email and Password.
- A logged-in session/token is used to authorize Task Create/View/Edit/Delete actions.
- Each task has at minimum a mandatory Title, with optional fields such as Description and Due Date.
- Standard field length limits and password complexity rules exist but are not explicitly defined in the assessment, so boundary test cases treat these as configurable/assumed limits to be confirmed against actual requirements.

No features beyond those explicitly listed in the assessment (e.g., password reset, notifications, sharing) have been assumed or tested.

## Potential Risks

See `Potential-Bugs.md` for the full list. At a summary level, the highest-impact risk areas identified through static analysis are:

- Missing or incomplete server-side validation
- Missing authorization checks on task-level operations (view/edit/delete)
- Lack of brute-force protection on login
- User enumeration through inconsistent error messaging
- Absence of confirmation before destructive actions (task deletion)
- Performance/scalability concerns with large task lists
- Lack of concurrency handling on simultaneous task edits

## Conclusion

This assessment demonstrates a structured QA approach to a multi-user CRUD application: translating a brief feature list into meaningful, well-organized test coverage, and proactively identifying realistic risk areas — particularly around authorization and data integrity — before any code is executed. The goal of this submission is to show **how I think and structure testing work**, in line with the assessment's evaluation criteria, rather than to claim exhaustive or guaranteed defect coverage.

## Repository Structure

```
.
├── README.md              # This file — assessment overview, approach, and analysis
├── Test-Cases.xlsx        # 53 detailed test cases across 8 modules + Summary sheet
└── Potential-Bugs.md      # 10 potential bugs/risk areas identified via static review
```

## Author

**[Munna Kumar]**
Software Tester (QA) — Assessment Submission
Email: [munna.kumar.cs.2023@mitmeerut.ac.in]
Submitted to: VirtuBox Infotech Private Limited
