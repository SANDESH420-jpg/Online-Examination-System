# System Architecture & UML Design Diagrams

This document presents 4 complete, renderable UML diagrams for the **Online Examination System**, constructed using [Mermaid.js](https://mermaid.js.org/).

---

## 1. Use Case Diagram

The Use Case diagram specifies the functional boundary of the system and primary actor interactions (Student, Instructor, Admin, and Auto-Proctor System).

```mermaid
graph TD
    %% Actors
    Student(("👤 Student"))
    Instructor(("👤 Instructor"))
    Admin(("👤 Administrator"))
    Proctor(("🤖 Auto-Proctor System"))

    subgraph SystemBoundary ["Online Examination System"]
        UC1["Login / Authenticate"]
        UC2["View Enrolled Courses"]
        UC3["Take Online Exam"]
        UC4["Auto-Save Answers"]
        UC5["View Score & Feedback"]
        
        UC6["Create & Manage Question Bank"]
        UC7["Schedule & Publish Exam"]
        UC8["Grade Descriptive Answers"]
        UC9["Generate Class Analytics"]
        
        UC10["Manage Users & Roles"]
        UC11["Audit Security Logs"]
        
        UC12["Monitor Tab Switching & Focus"]
        UC13["Auto-Submit on Violation / Timeout"]
    end

    %% Student Relationships
    Student --> UC1
    Student --> UC2
    Student --> UC3
    Student --> UC4
    Student --> UC5

    %% Instructor Relationships
    Instructor --> UC1
    Instructor --> UC6
    Instructor --> UC7
    Instructor --> UC8
    Instructor --> UC9

    %% Admin Relationships
    Admin --> UC1
    Admin --> UC10
    Admin --> UC11

    %% Proctor Relationships
    Proctor --> UC12
    Proctor --> UC13
    UC12 -.->|includes| UC13
    UC3 -.->|monitored by| UC12
```

---

## 2. Class Diagram

The Class diagram details the domain model, entity relationships, attribute types, and key operational methods.

```mermaid
classDiagram
    class User {
        +String userId
        +String username
        +String email
        +String passwordHash
        +Role role
        +login() Boolean
        +logout() Void
    }

    class Student {
        +String studentRegistrationId
        +String department
        +viewExams() List~Exam~
        +startExam(examId) ExamSession
    }

    class Instructor {
        +String employeeId
        +String designation
        +createQuestionBank() QuestionBank
        +createExam() Exam
        +evaluateSubmission(submissionId) Void
    }

    class Admin {
        +manageUser(userId) Void
        +viewAuditLogs() List~Log~
    }

    class Exam {
        +String examId
        +String title
        +DateTime startTime
        +DateTime endTime
        +Integer durationMinutes
        +Float totalMarks
        +Float passingMarks
        +Boolean isRandomized
        +publish() Void
    }

    class Question {
        +String questionId
        +String prompt
        +QuestionType type
        +Float maxMarks
        +Difficulty difficulty
        +addOption(option) Void
    }

    class Option {
        +String optionId
        +String text
        +Boolean isCorrect
    }

    class ExamSession {
        +String sessionId
        +DateTime startTimestamp
        +Integer remainingSeconds
        +SessionState state
        +Integer tabSwitchCount
        +autoSaveAnswer(questionId, response) Void
        +submitExam() EvaluationResult
    }

    class Answer {
        +String answerId
        +String questionId
        +String selectedOptionId
        +String textualResponse
        +Float scoreAssigned
    }

    class EvaluationResult {
        +String resultId
        +Float totalScoreObtained
        +String grade
        +Boolean statusPassed
        +DateTime evaluatedAt
    }

    %% Inheritance
    User <|-- Student
    User <|-- Instructor
    User <|-- Admin

    %% Associations & Aggregations
    Instructor "1" -- "*" Exam : creates
    Exam "1" *-- "*" Question : contains
    Question "1" *-- "*" Option : options
    Student "1" -- "*" ExamSession : executes
    ExamSession "1" -- "1" Exam : belongs to
    ExamSession "1" *-- "*" Answer : records
    ExamSession "1" -- "1" EvaluationResult : generates
```

---

## 3. Sequence Diagram (Exam Execution & Auto-Grading)

This diagram details the sequence of interactions when a student initializes, completes, auto-saves, and submits an online exam.

```mermaid
sequenceDiagram
    autonumber
    actor Student
    participant UI as Exam Client Interface
    participant Auth as Auth Service
    participant ExamSvc as Exam Engine
    participant Proctor as Proctoring Service
    participant DB as Database

    Student->>UI: Select Exam & Click "Start Exam"
    UI->>Auth: Validate JWT Session Token
    Auth-->>UI: Token Validated (Student Authorized)
    UI->>ExamSvc: Initialize Session (studentId, examId)
    ExamSvc->>DB: Fetch Exam & Shuffle Questions
    DB-->>ExamSvc: Return Question Package
    ExamSvc-->>UI: Return Question Set & Timer Config
    UI->>Student: Display Question 1 & Start Countdown Timer

    loop Exam Progress (Every 30s / Answer Click)
        Student->>UI: Select Option / Type Answer
        UI->>ExamSvc: API call POST /autosave (sessionId, questionId, answer)
        ExamSvc->>DB: Upsert Answer State
        DB-->>ExamSvc: Confirm Saved
        ExamSvc-->>UI: HTTP 200 OK (Status: "Saved")
    end

    opt Tab Switch / Focus Lost Event
        Student->>UI: Switch Tab / Unfocus Window
        UI->>Proctor: Log Event (tabSwitchCount + 1)
        Proctor-->>UI: Display Violation Alert Warning
    end

    alt Manual Submission OR Timer Expiration
        Student->>UI: Click "Submit Exam" (OR Timer = 0)
        UI->>ExamSvc: Final Submit Request (sessionId)
        ExamSvc->>ExamSvc: Auto-Grade MCQ & True/False Questions
        ExamSvc->>DB: Save Submission & Calculate Final Marks
        DB-->>ExamSvc: Saved Successfully
        ExamSvc-->>UI: Return Result Summary (Score, Pass/Fail)
        UI-->>Student: Display Exam Completed Confirmation Screen
    end
```

---

## 4. Activity Diagram (Student Exam Session Flow)

This diagram highlights the decision workflow, state transitions, security verification, and auto-submission mechanisms during an examination session.

```mermaid
flowchart TD
    Start([🚀 Start Exam Process]) --> LoginCheck{User Authenticated?}
    
    LoginCheck -- No --> RedirectLogin[Redirect to Login Page] --> EndSession([❌ End])
    LoginCheck -- Yes --> SelectExam[Select Available Exam from Dashboard]
    
    SelectExam --> TimeWindowCheck{Is Exam Window Active?}
    TimeWindowCheck -- No --> ShowWait[Display 'Exam Not Available' Message] --> DashboardReturn[Return to Dashboard]
    TimeWindowCheck -- Yes --> StartTimer[Initialize Session Timer & Lock Interface]
    
    StartTimer --> RenderQuestions[Display Questions & Navigation Palette]
    
    RenderQuestions --> EventLoop{Student Action / System Trigger}
    
    EventLoop -- Select/Edit Answer --> AutoSave[Trigger Background Auto-Save] --> UpdatePalette[Update Palette to 'Answered'] --> EventLoop
    
    EventLoop -- Flag Question --> MarkFlag[Set Status to 'Marked for Review'] --> EventLoop
    
    EventLoop -- Tab Switch Detected --> WarningCheck{Tab Switches >= 3?}
    WarningCheck -- No --> IncrementWarning[Show Warning Alert + Increment Count] --> EventLoop
    WarningCheck -- Yes --> AutoForceSubmit[🚨 Force Auto-Submit due to Security Violation]
    
    EventLoop -- Timer Expired --> AutoForceSubmit
    
    EventLoop -- Click Submit --> ConfirmSubmit{Confirm Submission?}
    ConfirmSubmit -- No --> EventLoop
    ConfirmSubmit -- Yes --> ProcessSubmit[Finalize Submission & Freeze UI]
    
    AutoForceSubmit --> ProcessSubmit
    
    ProcessSubmit --> AutoGrade[Evaluate Objective Questions Automatically]
    AutoGrade --> StoreResult[Store Answers & Scores in DB]
    StoreResult --> DisplaySummary[Display Score Summary & Completion Screen] --> Finish([✅ End Session])
```
