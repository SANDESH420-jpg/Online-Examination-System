# Software Requirements Specification (SRS)
## Project: Online Examination System

---

## 1. Introduction

### 1.1 Purpose
This document specifies the software requirements for the **Online Examination System**. It details functional and non-functional requirements, target user personas, system boundaries, and security standards to guide system architects, developers, and QA engineers throughout implementation.

### 1.2 Scope
The system is a cloud-ready web application providing end-to-end management of academic examinations. It empowers instructors to design assessments, enables students to securely take timed exams online, automates grading for objective question types, and presents analytical reports to administrators.

---

## 2. User Roles & System Actors

| User Role | Description & Permissions |
| :--- | :--- |
| **Student** | Registered learner authorized to view enrolled courses, take assigned exams, view real-time countdown timers, auto-save answers, and access post-exam score summaries. |
| **Examiner / Instructor** | Academic staff responsible for creating question banks, scheduling exams, defining passing criteria, reviewing subjective answers, and generating grade sheets. |
| **Administrator** | System admin responsible for user authentication management, course registration, system audit logging, security policy enforcement, and infrastructure health monitoring. |
| **System Proctor / Auto-Proctor** | Background background module enforcing anti-cheat policies (browser focus detection, tab-switch monitoring, session token validation). |

---

## 3. Functional Requirements

### 3.1 Authentication & User Management
- **FR-AUTH-01**: The system shall support secure password authentication with bcrypt password hashing and JWT session management.
- **FR-AUTH-02**: Role-Based Access Control (RBAC) must strictly enforce access limits based on user role (Student, Instructor, Admin).
- **FR-AUTH-03**: The system shall force single active session login per user to prevent concurrent credential sharing.

### 3.2 Exam Management & Question Bank
- **FR-EXAM-01**: Instructors shall be able to create question banks categorized by course, topic, and difficulty level (Easy, Medium, Hard).
- **FR-EXAM-02**: Instructors shall support multiple question formats:
  - Multiple Choice Questions (MCQ - single answer)
  - Multiple Select Questions (MSQ - multiple answers)
  - True / False
  - Short Text / Descriptive Answer
- **FR-EXAM-03**: Instructors shall configure exam duration, start/end date-time windows, total marks, passing threshold, and question randomization options.

### 3.3 Test Execution & Student Interface
- **FR-EXEC-01**: The student interface shall display a persistent countdown timer showing remaining time.
- **FR-EXEC-02**: The system shall auto-save student responses every 30 seconds and upon question navigation.
- **FR-EXEC-03**: Upon expiration of the exam timer, the system shall automatically freeze inputs and submit all saved answers.
- **FR-EXEC-04**: The system shall support a question palette allowing students to flag questions for review, navigate to specific question numbers, and view answered vs. unanswered status.

### 3.4 Security & Anti-Cheating (Proctoring)
- **FR-SEC-01**: The browser window shall monitor full-screen focus; switching tabs or minimizing the browser shall trigger warning alerts.
- **FR-SEC-02**: Exceeding 3 tab-switch warnings shall automatically auto-submit the exam with a flagged violation status.
- **FR-SEC-03**: Copy-paste, right-click context menus, and text selection shall be disabled on exam question pages.

### 3.5 Automated Grading & Analytics
- **FR-EVAL-01**: Objective questions (MCQ, True/False) must be graded automatically immediately upon submission.
- **FR-EVAL-02**: Instructors shall be provided an evaluation dashboard for manual review and marking of descriptive text answers.
- **FR-EVAL-03**: The system shall generate comprehensive analytics including class mean, median, standard deviation, and question-level difficulty index.

---

## 4. Non-Functional Requirements

### 4.1 Performance & Scalability
- **NFR-PERF-01**: Response time for question page loads and autosave API calls shall be under **500 ms** under peak load.
- **NFR-PERF-02**: The system shall support at least **1,000 concurrent active student test sessions** without performance degradation.

### 4.2 Security & Data Protection
- **NFR-SEC-01**: All data in transit must be encrypted using TLS 1.3 / HTTPS.
- **NFR-SEC-02**: All sensitive data at rest (user credentials, raw scores) must be encrypted using AES-256 standards.

### 4.3 Reliability & Availability
- **NFR-REL-01**: System availability shall maintain **99.5% uptime** during scheduled exam periods.
- **NFR-REL-02**: In the event of client-side internet disconnection, student progress must remain saved locally in browser storage and resume upon connection restoration.

### 4.4 Usability & Accessibility
- **NFR-USA-01**: The user interface shall adhere to WCAG 2.1 Level AA accessibility guidelines and be responsive across Desktop, Tablet, and Mobile devices.

---

## 5. User Stories & Acceptance Criteria

### User Story US-01: Exam Creation (Instructor)
> **As an** Instructor,  
> **I want to** create a randomized 30-question exam from my question bank with a 45-minute timer,  
> **So that** each student receives a unique sequence of questions.
- **Acceptance Criteria**:
  - Instructor can select question topics and difficulty distributions.
  - Questions are randomly sampled per student upon test initialization.
  - Exam cannot be published without setting start time, duration, and total marks.

### User Story US-02: Test Taking & Auto-Save (Student)
> **As a** Student,  
> **I want** my answers to auto-save periodically during the exam,  
> **So that** I don't lose progress if my browser unexpectedly refreshes.
- **Acceptance Criteria**:
  - Visual status indicator displays "Saved" with timestamp after each auto-save.
  - Refreshing the browser resumes the exact question state and remaining time.
