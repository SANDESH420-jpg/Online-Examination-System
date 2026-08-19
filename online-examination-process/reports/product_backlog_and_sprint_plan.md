# Product Backlog & Sprint Execution Plan

This document defines the Agile Product Backlog and 3-Sprint Execution Plan for the **Online Examination System**.

---

## 1. Product Backlog Overview

Tasks are estimated using Fibonacci Story Points (1, 2, 3, 5, 8, 13) based on implementation complexity, effort, and technical risk.

| ID | Epic | User Story / Feature Summary | Priority | Story Points | Target Sprint | Status |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: |
| **PB-01** | Architecture | System setup, directory layout, and CI/CD setup | High | 3 | Sprint 1 | ✅ Completed |
| **PB-02** | Requirements | Software Requirements Specification (SRS) | High | 5 | Sprint 1 | ✅ Completed |
| **PB-03** | Auth & RBAC | User Login, JWT Auth, & Role Management | High | 5 | Sprint 1 | ✅ Completed |
| **PB-04** | Design | System Architecture & UML Modeling (4 Diagrams) | High | 5 | Sprint 1 | ✅ Completed |
| **PB-05** | Question Bank| Question Bank CRUD & Category Tagging | High | 8 | Sprint 2 | ✅ Completed |
| **PB-06** | Exam Engine | Exam Scheduler & Configuration Interface | High | 8 | Sprint 2 | ✅ Completed |
| **PB-07** | Test UI | Student Exam Interface & Countdown Timer | High | 8 | Sprint 2 | ✅ Completed |
| **PB-08** | Auto-Save | Low-latency Auto-Save API & State Handler | Critical | 5 | Sprint 2 | ✅ Completed |
| **PB-09** | Proctoring | Tab-switch event monitoring & violation warnings | High | 8 | Sprint 3 | ✅ Completed |
| **PB-10** | Grading | Auto-grading engine for objective questions | High | 5 | Sprint 3 | ✅ Completed |
| **PB-11** | Testing | Test Cases Matrix & QA Suite Execution | High | 5 | Sprint 3 | ✅ Completed |
| **PB-12** | Reporting | Final Report, Gantt Chart, & Release Package | High | 3 | Sprint 3 | ✅ Completed |

---

## 2. Sprint Execution Plan

### 🏃 Sprint 1: Foundation, SRS & Design Architecture
- **Sprint Duration**: Week 1 - Week 2
- **Sprint Goal**: Establish system architecture, define SRS requirements, complete UML diagrams, and build secure user authentication services.
- **Velocity**: 18 Story Points
- **Deliverables**:
  - `README.md` & root repository structure
  - `requirements/requirements_document.md`
  - `design/uml_diagrams.md`
  - JWT Authentication Middleware & RBAC User Management

### 🏃 Sprint 2: Core Exam Engine, Question Bank & Test UI
- **Sprint Duration**: Week 3 - Week 4
- **Sprint Goal**: Build instructor question management, exam creation wizard, student test environment, countdown timer, and background auto-save API.
- **Velocity**: 29 Story Points
- **Deliverables**:
  - Question Bank Manager with MCQ / True-False support
  - Student Exam Execution Dashboard with persistent timer
  - Auto-save API endpoint (`POST /autosave`) with local storage fallback

### 🏃 Sprint 3: Proctoring, Automated Grading & Final Documentation
- **Sprint Duration**: Week 5 - Week 6
- **Sprint Goal**: Integrate anti-cheat proctoring logic, build objective auto-grading engine, execute QA test matrix, and construct final deliverables.
- **Velocity**: 21 Story Points
- **Deliverables**:
  - Browser tab-switch detection module with alert thresholds
  - Automated grading & score aggregation pipeline
  - `testing/Test_Cases_and_Matrix.xlsx`
  - `reports/gantt_chart.xlsx` & `reports/final_report.md`
