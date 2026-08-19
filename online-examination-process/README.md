# Online Examination System (Online Examination Process)

[![Project Status](https://img.shields.io/badge/Status-Active%20Development-blue.svg)](https://github.com/SANDESH420-jpg/Online-Examination-System)
[![Branch](https://img.shields.io/badge/Branch-sandesh-green.svg)](https://github.com/SANDESH420-jpg/Online-Examination-System/tree/sandesh)
[![License](https://img.shields.io/badge/License-MIT-orange.svg)]()

Welcome to the official repository for the **Online Examination System** course project. This repository contains the complete software development lifecycle artifacts—from initial requirements engineering and UML design diagrams to automated test suites, product backlogs, sprint reports, and final performance analytics.

---

## 📋 Table of Contents
1. [Project Overview](#-project-overview)
2. [Team Roles & Matrix](#-team-roles--matrix)
3. [Repository Directory Structure](#-repository-directory-structure)
4. [Commit Plan & Git Workflow](#-commit-plan--git-workflow)
5. [Getting Started](#-getting-started)

---

## 🎯 Project Overview
The **Online Examination System** is a secure, web-based platform designed to facilitate end-to-end examination management for educational institutions. The platform supports:
- **Secure Authentication & Role-Based Access**: Role management for Students, Instructors, and System Administrators.
- **Dynamic Question Bank & Exam Creation**: Support for Multiple Choice Questions (MCQ), True/False, Short Answer, and coding evaluations with randomized question ordering.
- **Real-Time Proctoring & Test Environment**: Active session tracking, tab-switching restrictions, auto-save timers, and strict anti-cheating mechanisms.
- **Automated Grading & Analytics**: Instant score generation for objective questions, automated feedback generation, and grade distribution analytics.

---

## 👥 Team Roles & Matrix

| Name | Role | Core Responsibilities |
| :--- | :--- | :--- |
| **Sandesh Chaudhary** | **Project Lead & Full-Stack Developer** | Architecture oversight, sprint planning, core module integration, and git workflow management. |
| **Team Member 2** | **System Architect & Backend Lead** | System design modeling, UML diagrams, database schema optimization, and API service development. |
| **Team Member 3** | **Requirements Specialist & UI/UX** | Software Requirements Specification (SRS), user persona definition, wireframing, and frontend styling. |
| **Team Member 4** | **QA Lead & Test Engineer** | Test case design, matrix execution, unit/integration test scripts, and defect tracking. |
| **Team Member 5** | **Scrum Master & Technical Writer** | Product backlog prioritization, sprint retrospectives, Gantt chart maintenance, and final report consolidation. |

---

## 📁 Repository Directory Structure

```text
online-examination-process/
├── README.md                               ← Team roles, repository structure, and commit plan
├── requirements/
│   ├── README.md                           ← Requirements documentation overview
│   └── requirements_document.md            ← Full Software Requirements Specification (SRS)
├── design/
│   ├── README.md                           ← Architecture & design system overview
│   └── uml_diagrams.md                     ← 4 comprehensive, renderable Mermaid UML diagrams
├── testing/
│   ├── README.md                           ← Testing methodology and matrix summary
│   └── test_cases_and_matrix.xlsx          ← Complete Excel test cases spreadsheet & execution matrix
└── reports/
    ├── README.md                           ← Project reports directory guide
    ├── gantt_chart.xlsx                    ← Interactive Excel Gantt chart & milestone tracker
    ├── product_backlog_and_sprint_plan.md  ← Agile product backlog & 3-sprint plan
    └── final_report.md                     ← Comprehensive final project summary & metrics
```

---

## 🔀 Commit Plan & Git Workflow

### Branching Conventions
- `main`: Production-ready release branch.
- `sandesh`: Core integration branch for active development and deliverable reviews.
- `feature/<feature-name>`: Isolated feature branches (e.g., `feature/exam-timer`, `feature/proctoring`).
- `fix/<bug-name>`: Bug fix branches.

### Commit Message Formatting
All commits follow the Conventional Commits specification:
```bash
<type>(<scope>): <short summary>

[optional body]
```
- **`feat`**: New feature introduced.
- **`fix`**: Bug fix.
- **`docs`**: Documentation changes (SRS, UML, Reports).
- **`test`**: Adding or updating test cases.
- **`refactor`**: Code reorganization without functional changes.

---

## 🚀 Getting Started

To explore or render the documentation locally:
1. Clone the repository branch:
   ```bash
   git clone -b sandesh https://github.com/SANDESH420-jpg/Online-Examination-System.git
   ```
2. Open `design/uml_diagrams.md` in any Markdown viewer supporting [Mermaid.js](https://mermaid.js.org/) to visualize system diagrams.
3. Open `.xlsx` files inside `testing/` and `reports/` in Microsoft Excel, LibreOffice Calc, or Google Sheets.
