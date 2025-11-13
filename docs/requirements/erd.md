# ERD — skillcheck (normalized)

This diagram shows the normalized schema for SkillCheck (roles, users, tests, questions, options, assignments, attempts, and user responses).<br>
PK / FK annotations are included for clarity.<br>

![ERD](../images/Mermaid%20Chart%20-%20Create%20complex,%20visual%20diagrams%20with%20text.-2025-11-13-062528.png)


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

# Index Reference — SkillCheck Database

This section lists all recommended **database indexes** for the SkillCheck platform along with their **purpose**.  
Indexes are created in **PostgreSQL** to improve read performance, especially on large datasets where filtering, joining, and sorting are frequent operations.  
All indexes below are designed to support **core system queries** while keeping write overhead minimal.  

<br>

## Table: `roles`
| Index Name | Columns | Type | Purpose |
|-------------|----------|------|----------|
| `roles_name_uq` | `(name)` | UNIQUE | Ensures that each role (Admin, Test Creator, Test Taker) has a unique name. Speeds up lookups by role name. |

<br>

## Table: `users`
| Index Name | Columns | Type | Purpose |
|-------------|----------|------|----------|
| `users_email_uq` | `(email)` | UNIQUE | Enforces unique email IDs for login and speeds up authentication queries. |
| `users_active_idx` | `(id)` with `WHERE deleted_at IS NULL` | Partial | Optimizes queries fetching active (non-deleted) users, reducing unnecessary scans. |

<br>

## Table: `roles_users`
| Index Name | Columns | Type | Purpose |
|-------------|----------|------|----------|
| `roles_users_user_id_idx` | `(user_id)` | Normal | Speeds up queries fetching all roles assigned to a specific user. |
| `roles_users_role_id_idx` | `(role_id)` | Normal | Improves performance when listing users under a specific role. |
| `roles_users_role_user_uq` | `(role_id, user_id)` | UNIQUE | Prevents duplicate role-user assignments and improves composite lookups. |

<br>

## Table: `tests`
| Index Name | Columns | Type | Purpose |
|-------------|----------|------|----------|
| `tests_created_by_idx` | `(created_by)` | Normal | Speeds up queries showing all tests created by a specific Test Creator. |
| `tests_status_created_at_idx` | `(status, created_at)` | Normal | Optimizes queries filtering tests by status and sorting by creation time. |
| `tests_title_trgm_idx` | `(title)` using `pg_trgm` | GIN | Enables fast text searches on test titles (for search/filter features). |

<br>

## Table: `questions`
| Index Name | Columns | Type | Purpose |
|-------------|----------|------|----------|
| `questions_test_id_idx` | `(test_id)` | Normal | Essential for retrieving all questions belonging to a given test. |
| `questions_test_id_created_at_idx` | `(test_id, created_at DESC)` | Composite | Speeds up queries ordering questions by creation date within a test. |
| `questions_question_text_ft_idx` | `to_tsvector('english', question_text)` | GIN | Enables full-text search in question content for advanced search features. |

<br>

## Table: `options`
| Index Name | Columns | Type | Purpose |
|-------------|----------|------|----------|
| `options_question_id_idx` | `(question_id)` | Normal | Speeds up retrieval of options belonging to a particular question. |

<br>

## Table: `test_assignments`
| Index Name | Columns | Type | Purpose |
|-------------|----------|------|----------|
| `test_assignments_user_id_idx` | `(user_id)` | Normal | Optimizes queries listing all tests assigned to a specific user. |
| `test_assignments_test_id_idx` | `(test_id)` | Normal | Improves performance for listing all users assigned to a specific test. |
| `test_assignments_test_user_uq` | `(test_id, user_id)` | UNIQUE | Prevents duplicate assignments of the same test to the same user. |

<br>

## Table: `test_attempts`
| Index Name | Columns | Type | Purpose |
|-------------|----------|------|----------|
| `test_attempts_user_id_idx` | `(user_id)` | Normal | Accelerates fetching all attempts by a particular user. |
| `test_attempts_test_id_idx` | `(test_id)` | Normal | Optimizes queries checking all attempts for a specific test. |
| `test_attempts_user_started_at_idx` | `(user_id, started_at)` | Composite | Speeds up queries that fetch recent attempts by a user (e.g., dashboard views). |
| `test_attempts_active_idx` | `(test_id)` with `WHERE ended_at IS NULL` | Partial | Helps quickly find active/incomplete attempts for live test tracking. |

<br>

## Table: `user_responses`
| Index Name | Columns | Type | Purpose |
|-------------|----------|------|----------|
| `user_responses_attempt_id_idx` | `(attempt_id)` | Normal | Improves retrieval of all responses within a single test attempt. |
| `user_responses_question_id_idx` | `(question_id)` | Normal | Speeds up performance when evaluating all answers for a given question. |
| `user_responses_user_attempt_question_idx` | `(user_id, attempt_id, question_id)` | Composite | Optimized for grading and checking user-specific responses during scoring. |
| `user_responses_attempt_q_opt_idx` | `(attempt_id, question_id)` INCLUDE `(option_id, is_correct)` | Covering | Helps in computing scores without reading full table rows, improving scoring performance. |

<br>

---



