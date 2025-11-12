# ERD — skillcheck (normalized)

This diagram shows the normalized schema for SkillCheck (roles, users, tests, questions, options, assignments, attempts, and user responses).<br>
PK / FK annotations are included for clarity.<br>

![ERD](../images/Mermaid%20Chart%20-%20Create%20complex,%20visual%20diagrams%20with%20text.-2025-11-11-074855.png)


# Database Schema Overview

The SkillCheck platform follows a **relational database structure** designed to manage users, roles, tests, and assessment data efficiently.  
This schema ensures data integrity, secure access control, and clear relationships between test creation, assignment, and evaluation processes.  

<br>

## 1. Roles and Users

- **roles** — Defines system-level roles such as *Admin*, *Test Creator*, and *Test Taker*.  
- **users** — Stores individual user details including name, email, and authentication credentials.  
- **roles_users** — Acts as a junction table to support a many-to-many relationship between users and roles, enabling flexible access management.  

<br>

## 2. Tests and Questions

- **tests** — Represents each test created within the system, including its title, description, duration, status, and the user who created it.  
- **questions** — Contains individual questions linked to a specific test. Each question references the correct option for validation.  
- **options** — Holds multiple-choice options for each question, one of which is marked as correct.  

<br>

## 3. Assignments and Attempts

- **test_assignments** — Manages which users are assigned to which tests.  
  Ensures that only authorized users can attempt specific assessments.  
- **test_attempts** — Records each attempt made by a user on a test, storing start and end times along with the calculated score.  

<br>

## 4. User Responses

- **user_responses** — Tracks individual question responses within each test attempt.  
  It logs the selected option, verifies correctness, and contributes to score calculation.  

<br>

## 5. Key Design Highlights

- Every table includes **created_at**, **updated_at**, and **deleted_at** timestamps for full auditability.  
- Foreign key constraints maintain relational consistency between users, tests, and responses.  
- Supports **multi-role user management**, **test versioning**, and **secure submission tracking**.  

<br>

This schema structure enables SkillCheck to maintain a clear and secure workflow — from **test creation and assignment** to **attempt evaluation and result recording** — while ensuring data consistency across all modules.
