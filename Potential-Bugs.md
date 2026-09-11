# Potential Bugs / Risk Areas — Task Management Application

**Important note:** The application was **not executed** as part of this assessment. The items below are **hypothetical risks identified through static analysis** of the described features (Registration, Login, Task CRUD, and the fact that tasks are stored in a database and tied to individual users). They are **not confirmed defects** — each one should be validated against the actual running application before being logged as a real bug.

---

### Bug ID: PB-01
**Module:** Registration / Login / Task CRUD (Cross-cutting)
**Bug Description:** Client-side validation may not be backed by equivalent server-side validation, allowing invalid or malicious data to be submitted directly via API calls (bypassing the UI).
**Severity:** Critical
**Reason / Impact:** If only the frontend validates input, an attacker can bypass it using browser dev tools or direct API requests, leading to bad data in the database, broken business rules, or injection-style attacks.
**Recommended Validation:** Attempt to submit invalid/malicious data directly to the backend API (bypassing the UI) and confirm the server independently rejects it with a proper error response.

---

### Bug ID: PB-02
**Module:** Task Edit / Task Delete / Task View
**Bug Description:** Authorization checks may be missing or incomplete on task-level operations, potentially allowing a logged-in user to view, edit, or delete another user's task by manipulating a task ID or request.
**Severity:** Critical
**Reason / Impact:** This is a broken access control risk. If present, it would allow unauthorized access to or tampering with another user's private data — a serious data privacy and security issue.
**Recommended Validation:** As User A, note a task ID; log in as User B and attempt to view/edit/delete User A's task ID directly (e.g., via URL or API manipulation). Confirm the request is blocked with an authorization error.

---

### Bug ID: PB-03
**Module:** Login
**Bug Description:** The login mechanism may not have rate-limiting, CAPTCHA, or account lockout after repeated failed attempts.
**Severity:** Major
**Reason / Impact:** Without this protection, the login page is vulnerable to brute-force password-guessing attacks, increasing the risk of account compromise.
**Recommended Validation:** Attempt several consecutive failed logins for the same account and confirm the system triggers a lockout, delay, or CAPTCHA after a defined threshold.

---

### Bug ID: PB-04
**Module:** Login / Registration
**Bug Description:** Error messages on login/registration may unintentionally reveal whether a specific email address is already registered (e.g., "Email not found" vs. "Incorrect password").
**Severity:** Major
**Reason / Impact:** This enables user enumeration, where an attacker can determine which emails are registered users — a privacy and security risk that can support targeted attacks.
**Recommended Validation:** Compare the error messages returned for "unregistered email" vs. "registered email + wrong password" and confirm they are identical/generic.

---

### Bug ID: PB-05
**Module:** Task Delete
**Bug Description:** Task deletion may not include a confirmation step, or may not clearly warn the user that the action is irreversible.
**Severity:** Major
**Reason / Impact:** Accidental deletion of important task data with no undo option leads to data loss and a poor user experience.
**Recommended Validation:** Attempt to delete a task and confirm a confirmation prompt appears; verify there is no way to accidentally trigger deletion with a single click.

---

### Bug ID: PB-06
**Module:** Task View/List
**Bug Description:** The task list may not implement pagination or lazy loading, which could cause slow load times or performance issues when a user has a large number of tasks.
**Severity:** Major
**Reason / Impact:** As the task count grows, page load time and responsiveness may degrade significantly, harming usability and potentially causing browser slowdowns or timeouts.
**Recommended Validation:** Populate a test account with a large number of tasks (e.g., 500–1000+) and measure page load time and UI responsiveness.

---

### Bug ID: PB-07
**Module:** Registration / Task Create
**Bug Description:** Rapid or repeated form submissions (e.g., double-clicking Register/Save) may not be debounced, potentially creating duplicate accounts or duplicate tasks.
**Severity:** Minor
**Reason / Impact:** Leads to duplicate/inconsistent records in the database and a confusing experience for the user (e.g., seeing the same task twice).
**Recommended Validation:** Double-click the Register/Save button in quick succession and confirm only one record is created, and/or that the button is disabled after the first click.

---

### Bug ID: PB-08
**Module:** Registration
**Bug Description:** Password policy (minimum length, complexity requirements) may be weak, inconsistently enforced, or not clearly communicated to the user.
**Severity:** Major
**Reason / Impact:** Weak passwords increase the risk of account compromise; unclear policy messaging leads to repeated failed registration attempts and poor UX.
**Recommended Validation:** Attempt registration with very short, common, or blank passwords and confirm consistent enforcement with a clear, specific error message.

---

### Bug ID: PB-09
**Module:** Login (Session Handling)
**Bug Description:** User sessions may not expire after a period of inactivity, or the expiry behavior may be inconsistent across the application.
**Severity:** Major
**Reason / Impact:** Sessions left active indefinitely increase the risk of unauthorized access on shared or public devices, and may allow stale/invalid sessions to continue performing actions.
**Recommended Validation:** Log in, remain idle beyond the expected timeout window, then attempt an action (e.g., create a task) and confirm the user is redirected to login with a session-expired message.

---

### Bug ID: PB-10
**Module:** Task Edit
**Bug Description:** Concurrent edits to the same task from two sessions/tabs may not be handled with any conflict detection (e.g., no versioning or optimistic locking), risking silent overwrites.
**Severity:** Minor
**Reason / Impact:** If two edits happen close together, one user's changes could silently overwrite the other's without warning, resulting in unnoticed data loss.
**Recommended Validation:** Open the same task in two sessions, edit and save in both with different values, and confirm the system either warns about the conflict or handles it in a predictable, documented way.

---

## Summary Table

| Bug ID | Module | Severity |
|--------|--------|----------|
| PB-01 | Cross-cutting (Validation) | Critical |
| PB-02 | Task Edit/Delete/View | Critical |
| PB-03 | Login | Major |
| PB-04 | Login/Registration | Major |
| PB-05 | Task Delete | Major |
| PB-06 | Task View/List | Major |
| PB-07 | Registration/Task Create | Minor |
| PB-08 | Registration | Major |
| PB-09 | Login (Session) | Major |
| PB-10 | Task Edit | Minor |

**Disclaimer:** All items above are risk hypotheses based on typical behavior of multi-user CRUD applications and the feature list provided in the assessment. None have been confirmed by executing the application. Each should be verified through actual test execution before being treated as a defect.
