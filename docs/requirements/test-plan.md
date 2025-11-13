# Testing Plan

This Testing Plan outlines how the SkillCheck platform will be tested to ensure that the main features work correctly and reliably.  
The goal is to keep testing simple while covering all important user flows of the MVP.

---

## 1. Goals of Testing
- Make sure all core features behave as expected.  
- Validate the main actions performed by Admin, Test Creator, and Test Taker.  
- Catch basic functional issues early during development.  
- Ensure the platform works smoothly from start to finish.

---

## 2. Types of Testing

### **Unit Testing**
Tests small, individual pieces of logic.

**Covers:**  
- Login and role checks  
- Creating tests  
- Adding questions  
- Starting and submitting attempts  

---

### **Integration Testing**
Tests how different parts of the system work together.

**Examples:**  
- Login → See dashboard  
- Create test → Add questions → Publish  
- Assign test → User sees assigned test  
- Start attempt → Submit → Score saved  

---

### **End-to-End Testing (E2E)**
Tests complete real-life user flows from the UI.

**Examples:**  
1. User logs in  
2. Creator creates and assigns a test  
3. Taker starts the test and submits  
4. Results page loads correctly  

---

## 3. Test Execution Approach
- Basic unit tests will be written for important logic.  
- Integration tests will check full flows between modules.  
- A few end-to-end tests will validate the major user journeys.  
- Tests will run automatically whenever code is pushed.

---

## 4. What Will Be Delivered
- Simple backend tests for core logic (auth, test creation, assignment).  
- Simple frontend tests for forms and main screens.  
- One or more end-to-end flows covering the full journey.  
- Automatic test runs through CI.

---

## 5. Coverage Goals
- Focus on core and high-risk areas.  
- Every major use case should be covered by at least one test.  
- Aim for stable behavior, not full coverage numbers.

---

## Summary

This testing approach keeps things lightweight while ensuring the main features of the SkillCheck MVP work correctly.  
More detailed testing can be added later as the platform grows.
