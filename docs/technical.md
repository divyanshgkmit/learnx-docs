# **Technical Docs - LearnX LMS**

## **1. Architecture Overview (AWS)**

**LearnX** is a role-based Learning Management System (LMS) connecting **Instructors** and **Students** through a secure, scalable web platform.
It follows a modular **MERN stack architecture** for seamless integration and deployment.

![logo](assets/aws.png)

## **2. Authentication Flow**

Authentication ensures that only valid **Instructors** and **Students** can access LearnX.
Users log in or sign up using email and password.

```mermaid
flowchart TD
    A[Open Login Page] --> B[Enter Email & Password]
    B --> C[Send Credentials to Server]
    C --> D[Verify in Database]
    D -->|Valid| E[Generate JWT Token]
    D -->|Invalid| F[Show Error Message]
    E --> G{User Role}
    G -->|Instructor| H[Redirect to Instructor Dashboard]
    G -->|Student| I[Redirect to Student Dashboard]
```

**Purpose:**

- Secure user login
- Prevent unauthorized access

---

## **3. Authorization Flow**

After login, the system checks the user’s role and grants access accordingly. Instructors can manage courses, while students can browse, enroll, and watch lessons.

```mermaid
flowchart TD
    A[Login Successful] --> B[Check Role]
    B -->|Instructor| C[Instructor Dashboard]
    C --> D[Create / Edit / Delete Courses]
    C --> E[View Enrolled Students]
    B -->|Student| F[Student Dashboard]
    F --> G[Browse & Enroll Courses]
    F --> H[Watch Lessons]
```

---

## **4. Tech Stack**

| **Layer** | **Logo** | **Technology** | **Version** |
|-----------|----------|----------------|-------------|
| **Programming Language** | <img src="https://skillicons.dev/icons?i=js" width="32" alt="JavaScript"/> | JavaScript | ES14 |
| **Frontend Library** | <img src="https://skillicons.dev/icons?i=react" width="32" alt="React"/> | React | 19.2.0 |
| **CSS Framework** | <img src="https://skillicons.dev/icons?i=tailwind" width="32" alt="Tailwind CSS"/> | Tailwind CSS | 4.1.17 |
| **Build Tool** | <img src="https://skillicons.dev/icons?i=vite" width="32" alt="Vite"/> | Vite | 7.2.2 |
| **Runtime Environment** | <img src="https://skillicons.dev/icons?i=nodejs" width="32" alt="Node.js"/> | Node.js | 22.12.0 |
| **Backend Framework** | <img src="https://skillicons.dev/icons?i=express" width="32" alt="Express"/> | Express | 5.1.0 |
| **Database** | <img src="https://skillicons.dev/icons?i=mongodb" width="32" alt="MongoDB"/> | MongoDB | 8.0 |
| **Media Storage** | <img src="https://raw.githubusercontent.com/tandpfun/skill-icons/231498caad5aa2ab9f05c4b6410fb5f7a8d3e424/icons/Cloudinary-Dark.svg" width="32" alt="Cloudinary"/> | Cloudinary | 1.45.0 |
| **Payment Integration (Test)** | <img src="https://cdn-icons-png.flaticon.com/128/174/174861.png" width="32" alt="PayPal"/> | PayPal SDK | 1.8.0 |
| **Authentication** | <img src="https://img.icons8.com/?size=96&id=rHpveptSuwDz&format=png" width="32" alt="JWT"/> | JWT | 9.0.2 |
| **Mobile Experience** | <img src="https://blog.openreplay.com/images/building-a-pwa-with-react/images/hero.png" width="32" alt="React+PWA"/> | React PWA | Manifest V3 |
| **Cloud Hosting** | <img src="https://skillicons.dev/icons?i=aws" width="32" alt="AWS"/> | AWS | Latest |
| **Version Control** | <img src="https://skillicons.dev/icons?i=github,githubactions" width="64" alt="GitHub"/> | GitHub | Latest |

---

## **5. Data Flow Diagram (DFD)**

The Data Flow Diagram (DFD) represents how data flows within the **LearnX LMS** platform. It visually explains how users (students and instructors) interact with the system and how data is processed, stored, and managed across different components.

---

### **DFD Level 0 - Context Diagram**

This level provides an overview of the complete system. It shows how **students** and **instructors** communicate with the **LearnX LMS**, which handles authentication, course management, and media storage using **MongoDB Atlas** and **Cloudinary**.

![logo](assets/dfd_level0.png)

---

### **DFD Level 1 - System Process Breakdown**

The Level 1 diagram expands the system into key functional processes **Authentication**, **Course Management**, and **Course Completion**. It illustrates how data moves between users, the database, and external services to support secure login, course handling, and student progress.

![logo](assets/dfd_level1.png)

---

## **6. Testing Plan**

Testing strategy to ensure all features work correctly

| **Area**              | **What to Test**                              | **Test Cases**                                                                 |
|-----------------------|-----------------------------------------------|--------------------------------------------------------------------------------|
| **Login Form**        | User can log in                               | - Valid email + password → login success<br>- Wrong password → show error<br>- Empty field → show error |
| **Registration**      | New user can sign up                          | - Fill all fields → account created<br>- Same email twice → error |
| **Course List**       | Shows courses                                 | - Page shows course cards<br>- Search box finds course by name<br>- No results → "Not found" message |
| **Course Details**    | Shows course info                             | - Title, price, instructor name visible<br>- Enroll button works |
| **Enrollment**        | User can join course                          | - Click Enroll → "You are enrolled" message |
| **Course Creation**   | Instructor adds course                        | - Click Publish → course appears in list |
| **API: Login**        | POST /auth/login                              | - Correct email/password → get token<br>- Wrong password → error |
| **API: Get Courses**  | GET /api/courses                              | - Returns list of courses<br>- Search works |

---

## **7. API Endpoints (Planned)**

### **Authentication APIs**
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `POST /api/auth/logout` - User logout
- `GET /api/auth/me` - Get current user

### **User APIs**
- `GET /api/users/profile` - Get user profile
- `PUT /api/users/profile` - Update user profile

### **Course APIs**
- `GET /api/courses` - Get all courses (with search/filter)
- `GET /api/courses/:id` - Get single course details
- `POST /api/courses` - Create new course (Instructor only)
- `PUT /api/courses/:id` - Update course (Instructor only)
- `DELETE /api/courses/:id` - Delete course (Instructor only)

### **Module APIs**
- `GET /api/courses/:id/modules` - Get course modules
- `POST /api/courses/:id/modules` - Add module to course
- `PUT /api/modules/:id` - Update module
- `DELETE /api/modules/:id` - Delete module

### **Enrollment APIs**
- `POST /api/enroll/:courseId` - Enroll in course (with test payment)
- `GET /api/enroll/my-courses` - Get enrolled courses

---

## **8. Conclusion**

**LearnX LMS** uses secure authentication and role-based authorization to provide:

- Clear separation of **Instructor** and **Student** views
- Safe and scalable system
- Ready for future features like progress tracking and payments
