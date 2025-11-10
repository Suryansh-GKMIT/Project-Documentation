# Use Case Document  
**Project:** SkillCheck – Enclosed Access Online Test Platform (MVP)

---

## 1. Business Overview
SkillCheck is an enclosed-access online assessment platform designed for organizations that need to conduct secure, internal tests for employees, trainees, or members. Unlike open public testing systems, SkillCheck operates within a controlled environment where all users are pre-registered and access is managed tightly by an Admin.
Organizations often rely on manual or fragmented methods to conduct internal assessments, resulting in inconsistencies, administrative overhead, and lack of centralized tracking. SkillCheck solves these problems by offering a structured test creation, assignment, and execution workflow.

---

## 2. Actors / Roles

### 2.1 Admin
Responsible for managing platform users, assigning permissions, and overseeing tests and results.

### 2.2 Test Creator
Authorized user who can create tests, add questions, assign Test Takers, and view results.

### 2.3 Test Taker
End user who logs in to attempt tests assigned to them.

---

## 3. Preconditions
1. Test Takers must be registered users.
2. Test Creators must assign Test Takers before tests become visible to them.
3. Tests must contain at least one question before being published.


---

## 4. Use Cases

```mermaid
flowchart LR
    %% Actors
    subgraph Actors
      A[Admin]
      C[Test Creator]
      T[Test Taker]
    end

    %% Use Cases
    UC1["UC1\nManage Users"]
    UC2["UC2\nGrant Creator Access"]
    UC3["UC3\nCreate Test"]
    UC4["UC4\nAdd / Edit Questions"]
    UC5["UC5\nAssign Test Takers"]
    UC6["UC6\nPublish Test"]
    UC7["UC7\nView Results (by Test)"]
    UC12["UC12\nView Results (by User)"]
    UC8["UC8\nView All Results / Admin Dashboard"]
    UC9["UC9\nView Assigned Tests (Taker)"]
    UC10["UC10\nAttempt Test"]
    UC11["UC11\nSubmit Test"]
    UC13["UC13\nView Own Results"]

    %% Links
    A --- UC1
    A --- UC2
    A --- UC8

    C --- UC3
    C --- UC4
    C --- UC5
    C --- UC6
    C --- UC7
    C --- UC12

    T --- UC9
    T --- UC10
    T --- UC11
    T --- UC13

    %% Style
    classDef actor fill:#f2f2f2,stroke:#333,stroke-width:1px;
    class A,C,T actor;

```
<br>
<br>

### **UC1 – Manage Users**
**Actor:** Admin  
**Preconditions:** Admin is logged in.  
**Main Flow:**<br>
1. Admin opens “User Management.”<br>
2. Adds, edits, or deletes user accounts.<br>
3. Updates user status (active/inactive).<br>
**Postcondition:** User data updated in database.<br>
**Exceptions:** Invalid details or duplicate email found.

---

### **UC2 – Grant Creator Access**
**Actor:** Admin  
**Preconditions:** Admin authenticated and user exists.<br>
**Main Flow:**<br>
1. Admin selects an existing user.<br>
2. Grants “Test Creator” access.<br>
3. Saves permission changes.<br>
**Postcondition:** User promoted to Creator role.<br>
**Exceptions:** User already has creator access.

---

### **UC3 – Create Test**
**Actor:** Test Creator  
**Preconditions:** Creator authenticated and has permissions.<br>
**Main Flow:**<br>
1. Creator logs in and clicks “Create Test.”<br>
2. Enters test title, duration, and description.<br>
3. Saves the test in Draft status.<br>
**Postcondition:** Test saved successfully in Draft state.<br>
**Exceptions:** Missing required input fields.

---

### **UC4 – Add / Edit Questions**
**Actor:** Test Creator  
**Preconditions:** Test exists in Draft state.<br>
**Main Flow:**<br>
1. Creator opens test in edit mode.<br>
2. Adds questions with text, options, and correct answers.<br>
3. Edits or deletes questions as needed.<br>
4. Saves changes.<br>
**Postcondition:** Questions successfully added or modified.<br>
**Exceptions:** Validation error – incomplete question data.

---

### **UC5 – Assign Test Takers**
**Actor:** Test Creator  
**Preconditions:** Test created and users available.<br>
**Main Flow:**<br>
1. Creator navigates to “Assign Users.”<br>
2. Selects users from system list.<br>
3. Assigns selected users to the test.<br>
4. Saves assignments.<br>
**Postcondition:** Test Takers linked to the test.<br>
**Exceptions:** No user selected or assignment failed.

---

### **UC6 – Publish Test**
**Actor:** Test Creator  
**Preconditions:** Test must have at least one question.<br>
**Main Flow:**<br>
1. Creator opens test from Drafts.<br>
2. Clicks “Publish.”<br>
3. System validates test data.<br>
**Postcondition:** Test published and visible to assigned users.<br>
**Exceptions:** No questions → Publish blocked.

---

### **UC7 – View Results (by Test)**
**Actor:** Test Creator  
**Preconditions:** At least one test attempt exists.<br>
**Main Flow:**<br>
1. Creator opens “Results.”<br>
2. Selects a test.<br>
3. Views all submissions and scores.<br>
4. Optionally exports results as CSV.<br>
**Postcondition:** Results displayed per test.<br>
**Exceptions:** No attempts found.

---

### **UC8 – View All Results / Admin Dashboard**
**Actor:** Admin  
**Preconditions:** Admin authenticated.<br>
**Main Flow:**<br>
1. Admin opens “Dashboard.”<br>
2. Views system-wide test data (users, tests, attempts).<br>
3. Analyzes performance metrics.<br>
**Postcondition:** Summary metrics displayed.<br>
**Exceptions:** Data unavailable or incomplete.

---

### **UC9 – View Assigned Tests**
**Actor:** Test Taker  
**Preconditions:** User has assigned tests.<br>
**Main Flow:**<br>
1. Test Taker logs in.<br>
2. Opens “Assigned Tests.”<br>
3. System lists all active tests.<br>
**Postcondition:** Assigned tests visible.<br>
**Exceptions:** No active tests.

---

### **UC10 – Attempt Test**
**Actor:** Test Taker  
**Preconditions:** Test assigned and Active.<br>
**Main Flow:**<br>
1. Test Taker clicks “Start Test.”<br>
2. Timer begins.<br>
3. Answers questions sequentially.<br>
4. System auto-saves progress.<br>
**Postcondition:** Attempt created and responses stored.<br>
**Exceptions:** Network disconnection or timeout.

---

### **UC11 – Submit Test**
**Actor:** Test Taker  
**Preconditions:** Attempt in progress.<br>
**Main Flow:**<br>
1. User clicks “Submit.”<br>
2. System validates answers and stops timer.<br>
3. Calculates score and saves record.<br>
**Postcondition:** Attempt marked “Completed.”<br>
**Exceptions:** Server error or timeout during submission.

---

### **UC12 – View Results (by User)**
**Actor:** Test Creator / Admin  
**Preconditions:** User has completed at least one test.<br>
**Main Flow:**<br>
1. Opens “Results by User.”<br>
2. Selects a specific user.<br>
3. System lists tests attempted and corresponding scores.<br>
**Postcondition:** User’s performance history displayed.<br>
**Exceptions:** User has no test attempts.

---

### **UC13 – View Own Results**
**Actor:** Test Taker (Web or Mobile App)<br>
**Preconditions:** Test Taker has completed at least one test.<br>
**Main Flow:**<br>
1. Logs in via web or mobile app.<br>
2. Opens “My Results.”<br>
3. System fetches completed attempts.<br>
4. Displays scores, test names, and completion dates.<br>
**Postcondition:** Results visible to logged-in user.<br>
**Exceptions:** No completed attempts found.

---

## 5. Future Scope Use Cases
1. Tab-switch and window-switch monitoring.
2. Camera and microphone requirements.
3. Face detection and cheating flagging.
4. Live proctoring dashboard.
5. Randomized question order per attempt.
