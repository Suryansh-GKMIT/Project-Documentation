# SkillCheck – Enclosed Access Online Test Platform (MVP)

**SkillCheck** is a secure, closed-access online testing platform designed to manage and deliver assessments within an organization.<br>
It provides controlled access to tests, user role management, automated grading, and detailed result tracking — ensuring integrity, scalability, and seamless user experience for all participants.

---

## System Overview

The platform operates within a restricted environment where only authorized users can access the system.<br>
It supports three primary roles:

- **Admin** – Manages users, assigns roles (Test Creator / Test Taker), oversees the entire system, and monitors test performance.  
- **Test Creator** – Designs, edits, and publishes tests, adds questions and options, assigns tests to users, and reviews test results.  
- **Test Taker** – Attempts assigned tests, views scores, and accesses personal result history.

All actions and data are securely handled through a single centralized database, ensuring traceability and consistency across the system.

---

## Core Features

- **User & Role Management** – Controlled access managed by Admin; role-based permissions (Admin, Creator, Taker).  
- **Test Creation & Editing** – Test Creators can build, modify, and preview tests with multiple question types.  
- **Assignments** – Tests can be selectively assigned to specific users or groups.  
- **Attempt Lifecycle** – Test Takers can start and submit their test attempts.  
- **Automated Grading & Reports** – System automatically evaluates answers and generates results accessible to creators and admins.  
- **Secure Data Flow** – Every operation (from login to submission) interacts with the centralized PostgreSQL database through secure APIs.  
- **Responsive PWA Interface** – Optimized for both web and mobile usage in a controlled internal network.  

---

## Technology Stack

- **Frontend:** React 19 (PWA) + Vite 7   
- **Backend:** Node.js 24 (LTS) + Express 5 + prisma ORM  
- **Database:** PostgreSQL 17 (RDS – AWS)  
- **Authentication:** JWT-based role control    
- **Infrastructure:** AWS ( RDS, EC2)

---

## System Objectives

1. To provide an internal, secure platform for test management and evaluation.  
2. To ensure reliable user access control with distinct roles and permissions.  
3. To automate test grading, result generation, and report delivery.  
4. To maintain full data integrity through centralized database storage and controlled access.  

---

## Data Flow Summary

1. **Admin** manages users and assigns roles.<br>
2. **Test Creator** creates and publishes tests.<br>
3. **Test Taker** attempts assigned tests.<br>
4. All operations read/write to a single PostgreSQL database.<br>
5. Results are computed, stored, and presented securely.

**SkillCheck** aims to deliver a robust, maintainable, and secure testing ecosystem tailored for organizational use.
