# Software Tester (QA) Assessment

![QA Testing](https://img.shields.io/badge/Role-Software%20Tester%20%28QA%29-blue)
![Testing](https://img.shields.io/badge/Testing-Functional%20%7C%20Validation%20%7C%20Security-green)
![Status](https://img.shields.io/badge/Status-Assessment-orange)

## 📌 Overview

This repository contains my submission for the **Software Tester (QA) Assessment**.

The assessment is based on a **Task Management Application** that is assumed to be close to production release and has no existing test documentation.

The objective is to demonstrate a structured QA approach by designing test scenarios, test cases, and identifying potential bugs and risk areas before production release.

---

## 🎯 Assessment Objectives

The main objectives of this assessment are:

- Design structured test scenarios and test cases.
- Cover positive, negative, and edge cases.
- Test user registration and login functionality.
- Test Task CRUD operations.
- Verify input validation and error handling.
- Identify potential bugs and risk areas.
- Assign appropriate severity to identified risks.
- Consider security, authorization, and data integrity.

---

## 🧩 Application Under Test

The application is a **Task Management Application** with the following features:

### 🔐 User Authentication

- User Registration
- User Login

### 📝 Task Management

Authenticated users can:

- Create a task
- View task list
- Edit a task
- Delete a task

### 💾 Database

- Tasks are stored in a database.
- Stored tasks are displayed in a task list.

---

# 🧪 Test Scope

The following areas are covered in this assessment:

| Module | Testing Coverage |
|---|---|
| Registration | Positive, Negative & Edge Cases |
| Login | Positive, Negative & Edge Cases |
| Create Task | Positive, Negative & Edge Cases |
| View Task List | Functional & Authorization Testing |
| Edit Task | Positive, Negative & Edge Cases |
| Delete Task | Positive, Negative & Edge Cases |
| Input Validation | Empty, Invalid & Boundary Inputs |
| Error Handling | Application & Server Error Scenarios |
| Security | Authentication & Authorization Risks |
| Data Persistence | Database & Refresh Scenarios |

---

# 📋 Test Case Design

## 1. Registration Testing

The registration functionality should be tested for:

- Valid registration details.
- Empty required fields.
- Invalid email formats.
- Duplicate email addresses.
- Weak passwords.
- Password confirmation.
- Special characters.
- Leading and trailing spaces.
- Maximum-length inputs.
- Extremely long inputs.

### Example Test Case

| Test Case ID | Scenario | Expected Result | Type |
|---|---|---|---|
| REG-01 | Register with valid details | Account should be created successfully | Positive |
| REG-02 | Register with empty email | Validation message should be displayed | Negative |
| REG-03 | Register with existing email | Registration should be rejected | Negative |
| REG-04 | Register with invalid email | Invalid email message should appear | Negative |
| REG-05 | Register with maximum-length input | Application should handle input correctly | Edge |

---

## 2. Login Testing

The login functionality should be tested for:

- Valid credentials.
- Incorrect password.
- Unregistered email.
- Empty email.
- Empty password.
- Invalid email format.
- Case sensitivity.
- Leading/trailing spaces.
- Multiple failed login attempts.

### Example Test Case

| Test Case ID | Scenario | Expected Result | Type |
|---|---|---|---|
| LOG-01 | Login with valid credentials | User should login successfully | Positive |
| LOG-02 | Login with wrong password | Login should fail with an error message | Negative |
| LOG-03 | Login with unregistered email | Login should fail | Negative |
| LOG-04 | Login with empty fields | Required-field validation should appear | Negative |
| LOG-05 | Multiple failed login attempts | Application should handle repeated failures securely | Edge |

---

# 📝 3. Task CRUD Testing

CRUD stands for:

- **C — Create**
- **R — Read**
- **U — Update**
- **D — Delete**

## Create Task

Test whether an authenticated user can create tasks using valid information.

Test cases should also verify:

- Empty task title.
- Spaces-only title.
- Very long title.
- Special characters.
- Duplicate tasks.
- Creating a task without authentication.

---

## Read / View Task

Verify that:

- User can view their task list.
- Correct task information is displayed.
- Multiple tasks are displayed correctly.
- Empty task list is handled properly.
- Deleted tasks do not reappear.
- Users cannot access another user's tasks.

---

## Update / Edit Task

Verify that:

- Existing tasks can be edited.
- Task title can be updated.
- Task description can be updated.
- Required fields are validated.
- Updated data persists after refresh.
- Users cannot edit another user's tasks.

---

## Delete Task

Verify that:

- Existing tasks can be deleted.
- Delete confirmation works correctly.
- Canceling deletion keeps the task.
- Deleted tasks disappear from the list.
- Deleted tasks remain deleted after refresh.
- Users cannot delete another user's tasks.

---

# 🔍 4. Input Validation & Error Handling

The following validation and error scenarios should be considered:

- Empty fields.
- Invalid email format.
- Invalid task information.
- Spaces-only input.
- Very long input.
- Special characters.
- Invalid task IDs.
- Unauthorized requests.
- Database errors.
- Server errors.
- Network failures.
- Clear and understandable error messages.

The application should handle invalid input gracefully instead of crashing or exposing technical information.

---

# 🐞 Potential Bugs & Risk Areas

The following are **potential bugs/risk areas identified without executing the application**.

| Bug ID | Potential Bug | Severity | Reason / Impact |
|---|---|---|---|
| BUG-01 | Duplicate email allowed during registration | Major | May create duplicate accounts and data inconsistency |
| BUG-02 | Unauthorized user can access task data | Critical | Private user information may be exposed |
| BUG-03 | User can modify another user's task | Critical | Causes authorization and data integrity issues |
| BUG-04 | Deleted task appears again after refresh | Major | May indicate a database persistence issue |
| BUG-05 | Empty or spaces-only task title is accepted | Major | Invalid records may be stored |
| BUG-06 | Invalid input causes server/application error | Major | Can affect application stability |
| BUG-07 | Edited task changes are lost after refresh | Major | Users may lose their updates |
| BUG-08 | Incorrect login credentials are accepted | Critical | Can allow unauthorized account access |
| BUG-09 | Extremely long input breaks the UI | Minor | May affect usability and interface stability |
| BUG-10 | Technical/database error details are exposed | Major | Sensitive implementation information may be revealed |

---

# 🔐 Security & Authorization Considerations

Security is an important testing area for a task management application.

The following scenarios should be verified:

- Unauthenticated users should not access protected task functionality.
- Users should only be able to access their own tasks.
- Users should not be able to edit another user's task.
- Users should not be able to delete another user's task.
- Invalid or manipulated task IDs should be handled safely.
- Login failures should not expose sensitive information.
- Server/database errors should not expose technical details.

---

# 🔄 Testing Flow

```text
User Registration
       ↓
User Login
       ↓
Authentication Verification
       ↓
Create Task
       ↓
View Task List
       ↓
Edit Task
       ↓
Delete Task
       ↓
Refresh & Data Persistence
       ↓
Input Validation
       ↓
Error Handling
       ↓
Authorization & Security Checks
