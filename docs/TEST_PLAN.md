# Test Plan: SSCentral In-Game API

This document describes the test plan used to audit and verify the **SSCentral In-Game API**, the backend platform that supports the mobile game *FiveSteps: Rhythm Game*.

The plan describes the testing objectives, test scope, test environment, testing strategy, execution workflow, and entry and exit criteria used during the QA cycle.

---

## 1. Objectives

The main goals of this testing effort are:

* Verify that all In-Game API endpoints work correctly under normal and edge-case conditions.
* Ensure proper authentication and authorization checks across protected routes using JWT validation.
* Validate input parameters, boundary values, pagination limits, and sorting features.
* Identify backend defects and test script issues through failure analysis.
* Fix the identified API defects and correct test cases when the failure was caused by an incorrect assertion.
* Perform a full regression test run after the fixes and confirm a stable 100% pass rate.

---

## 2. Test Scope

### 2.1. In-Scope (Modules Tested)

The test suite focuses on the **In-Game Module**, which contains the main features used by active players on a daily basis.

| # | Folder / Submodule | Description | Requests |
| :--- | :--- | :--- | :--- |
| **00** | **Player Authentication** | Handles Firebase authentication and retrieves the player JWT used by protected endpoints. | 1 |
| **01** | **Song Discovery** | Tests song listing, search queries, sorting, pagination, and boundary limits. | 26 |
| **02** | **Voting** | Validates song and pack voting, duplicate votes, and content status restrictions. | 15 |
| **03** | **Hash Verification** | Tests SSC chart hash verification and authentication enforcement. | 15 |
| **04** | **Song Download** | Checks song file download permissions and error handling. | 6 |
| **05** | **HUB & Community Packs** | Tests browsing of featured and community song packs. | 6 |
| **Total** | **Full In-Game Suite** | **Complete In-Game API test coverage.** | **69 Requests** |

> **Note:** The suite contains **69 API requests** and **137 assertions**. A single API request can contain multiple assertions to validate status codes, response data, schemas, and business rules.

### 2.2. Out-of-Scope

The following areas were excluded from this specific test cycle:

* Creator Module endpoints.
* Moderation Admin Module endpoints.
* Mobile App frontend UI testing.
* Performance and load testing.

---

## 3. Test Environment & Tools

| Component | Tool / Technology |
| :--- | :--- |
| **API Under Test** | SSCentral API (`v2`) running locally at `http://127.0.0.1:8787` |
| **Environment File** | `SSCENTRAL-LOCAL.postman_environment.json` |
| **Test Client** | Postman (Collection v2.1) |
| **CLI Runner** | Newman CLI |
| **Reporting Tool** | `newman-reporter-htmlextra` |
| **Authentication** | Firebase Auth with Bearer JWT tokens |
| **Database** | Pre-seeded local test dataset |

---

## 4. Test Strategy & Types of Testing

The testing process used an **automated API and integration testing** approach.

### 4.1. Functional Testing

Validates that API endpoints return the expected HTTP status codes, JSON response structures, data fields, and values.

### 4.2. Negative & Boundary Testing

Tests invalid input and edge cases, including:

* Invalid data types.
* Negative pagination values such as `limit=-1`.
* Invalid or missing parameters.
* Non-existent IDs.
* Empty or missing request data.

The goal is to verify that the API handles invalid input correctly and returns appropriate error responses.

### 4.3. Security & Authentication Testing

Tests protected endpoints using different authentication conditions, including:

* Missing Bearer tokens.
* Invalid tokens.
* Expired tokens.
* Requests without the `Authorization` header.

The goal is to verify that protected endpoints reject unauthorized requests with the correct HTTP status codes, such as `401 Unauthorized`.

### 4.4. Business Logic Testing

Validates application rules and expected behavior based on the state of the data.

Examples include:

* Preventing votes on unapproved songs.
* Preventing duplicate votes.
* Validating song and pack status.
* Checking restrictions based on user or content state.

### 4.5. Regression Testing

After the identified API defects were fixed and the incorrect test assertions were updated, the complete test suite was executed again.

The goal was to confirm that:

* The reported defects were fixed.
* The corrected test cases passed.
* Existing functionality was not affected by the changes.
* The complete suite finished with zero failing assertions.

---

## 5. Test Execution Workflow

The project followed a two-phase testing cycle.

### Phase 1 — Initial Audit (Baseline)

The Postman collection was executed against the initial version of the local API.

The baseline execution included:

* **69 API requests**
* **137 assertions**
* **91 passed assertions**
* **46 failed assertions**

### Phase 2 — Failure Analysis

Each failed assertion was reviewed to determine the cause of the failure.

The failures were classified into two main groups:

* **Actual API defects:** Problems found in the backend implementation.
* **Test design issues:** Failures caused by incorrect test expectations or assertions.

This analysis helped separate real API problems from issues in the test suite itself.

### Phase 3 — Remediation

The identified issues were addressed based on their cause:

* API defects were fixed in the backend code.
* Incorrect test assertions were updated to match the expected API behavior.
* Test cases were reviewed to make sure they were stable and based on valid test data.

### Phase 4 — Regression Run

The complete Postman collection was executed again using Newman CLI.

The regression run was used to verify that:

* The API defects were fixed.
* The updated test cases passed.
* No new failures were introduced.
* The complete test suite achieved a 100% pass rate.

---

## 6. Entry and Exit Criteria

### 6.1. Entry Criteria

Testing could start when the following conditions were met:

* The local API server was running and accessible.
* The database was populated with the required test data.
* Valid and unapproved song records were available for testing.
* Required chart hashes were available in the database.
* Test user accounts were available.
* The Postman collection was configured correctly.
* The Postman environment file was loaded with the required variables.
* Authentication tokens could be generated successfully.

### 6.2. Exit Criteria

The test cycle was considered complete when:

* 100% of the planned test cases were executed.
* All critical and high-severity API defects were fixed and verified.
* Test design issues identified during failure analysis were corrected.
* The final Newman regression execution had zero failing assertions.
* The final regression result reached **137/137 passed assertions (100%)**.

---

## 7. Test Results Summary

| Metric | Initial Audit (Baseline) | Final Regression Run |
| :--- | :--- | :--- |
| **Total API Requests** | 69 | 69 |
| **Total Assertions** | 137 | 137 |
| **Passed Assertions** | 91 (66.4%) | 137 (100%) |
| **Failed Assertions** | 46 (33.6%) | 0 (0%) |
| **Total Run Duration** | ~7.0 seconds | ~6.9 seconds |
| **Final Suite Status** | Failed | Passed |

### Initial Audit

The initial execution found **46 failed assertions out of 137**.

The failures were reviewed individually to identify the root cause and determine whether each failure represented an actual API defect or an issue in the test suite.

### Final Regression

After fixing the identified API defects and correcting the test assertions, the complete suite was executed again.

The final regression run achieved:

> **137/137 assertions passed — 100% pass rate**

No failing assertions remained in the final regression execution.

---

## 8. Final Test Status

**Test Cycle Status: PASSED**

The SSCentral In-Game API test suite completed the QA cycle successfully.

The testing process covered functional behavior, negative and boundary cases, authentication, authorization, business logic, and regression testing.

The initial execution helped identify both backend defects and issues in the test suite. After the required fixes and test updates, the final regression run completed with **zero failed assertions and a 100% pass rate**.