# Software Testing & Verification (`testing/`)

This directory contains the testing methodology, test suite execution matrix, and test case documentation for the **Online Examination System**.

## Directory Contents
- [`test_cases_and_matrix.xlsx`](file:///Users/sandeshchaudhary/Desktop/Testing/testing/test_cases_and_matrix.xlsx): Comprehensive Excel spreadsheet containing detailed test cases, execution status, defect tracking, and traceability matrix.

## Testing Strategy Overview

The testing phase follows a multi-layered verification strategy:

| Test Level | Scope | Primary Objective |
| :--- | :--- | :--- |
| **Unit Testing** | Individual API functions & components | Validate logic correctness of score calculation, timer countdowns, and token validation. |
| **Integration Testing** | API & Database interaction | Ensure seamless data flow between authentication service, question bank, and submission engine. |
| **Security & Proctoring Testing** | Anti-cheating & Session integrity | Verify tab-switch detection, browser focus event listeners, and concurrent login prevention. |
| **User Acceptance Testing (UAT)** | End-to-end user workflows | Validate exam workflow from student, instructor, and admin perspectives. |

## Test Execution Summary Matrix

| Module / Feature | Total Test Cases | Passed | Failed | Blocked | Pass Rate (%) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Authentication & RBAC** | 12 | 12 | 0 | 0 | 100% |
| **Exam Creation & Question Bank** | 18 | 18 | 0 | 0 | 100% |
| **Student Test Engine & Auto-Save** | 25 | 25 | 0 | 0 | 100% |
| **Anti-Cheat & Proctoring** | 15 | 14 | 1 | 0 | 93.3% |
| **Automated Grading & Reports** | 15 | 15 | 0 | 0 | 100% |
| **TOTAL** | **85** | **84** | **1** | **0** | **98.8%** |
