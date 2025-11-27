# **Testing Plan**

## **1. Registration Tests**

| **TC-ID**  | **Scenario**        | **Test Steps**                              | **Expected**                                  |
| ---------- | ------------------- | ------------------------------------------- | --------------------------------------------- |
| **REG-01** | Student Register    | Fill valid student data and Submit     | Account created, redirect to dashboard        |
| **REG-02** | Instructor Register | Fill valid instructor data and Submit  | Account created, redirect to instructor panel |
| **REG-03** | Duplicate Email     | Use existing email and Submit          | Error: "Email already exists"                 |
| **REG-04** | Invalid Email       | Enter invalid email format and Submit       | Validation error                              |

---

## **2. Login Tests**

| **TC-ID**    | **Scenario**      | **Test Steps**                                        | **Expected**                        |
| ------------ | ----------------- | ----------------------------------------------------- | ----------------------------------- |
| **LOGIN-01** | Student Login     | Valid credentials and Submit                     | JWT received, student dashboard     |
| **LOGIN-02** | Instructor Login  | Valid credentials and Submit                     | JWT received, instructor panel      |
| **LOGIN-03** | Wrong Password    | Valid email + wrong password and Submit          | Error: "Invalid credentials"        |
| **LOGIN-04** | Empty Credentials | Leave fields blank and Submit                    | Validation errors                   |

---

## **3. Authorization Tests**

| **TC-ID**   | **Scenario**                | **Test Steps**                                        | **Expected**            |
| ----------- | --------------------------- | ----------------------------------------------------- | ----------------------- |
| **AUTH-01** | Student Access              | Login as student and Access student routes       | Access granted          |
| **AUTH-02** | Instructor Access           | Login as instructor and Access instructor routes | Access granted          |
| **AUTH-03** | Student → Instructor Routes | Login as student and Access instructor routes    | Access denied (403)     |

---

## **4. Test Implementation**

**Frontend Unit Tests**
- Form validation
- UI state management
- Component rendering

**Integration Tests**
- API calls with mock responses
- End-to-end user flows
- Error handling

**Test Data**
```javascript
const testUsers = {
  student: { email: "student@test.com", password: "123456" },
  instructor: { email: "instructor@test.com", password: "123456" }
};
```