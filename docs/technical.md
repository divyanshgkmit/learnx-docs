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
    C --> D[Create / Edit / Delete Courses & Modules]
    B -->|Student| F[Student Dashboard]
    F --> G[Browse & Enroll Courses]
    F --> H[Watch Lessons]
```

---

## **4. Tech Stack**

| **Layer**                      | **Logo**                                                                                                                                                           | **Technology** | **Version** |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------- | ----------- |
| **Programming Language**       | <img src="https://skillicons.dev/icons?i=js" width="32" alt="JavaScript"/>                                                                                         | JavaScript     | ES14        |
| **Frontend Library**           | <img src="https://skillicons.dev/icons?i=react" width="32" alt="React"/>                                                                                           | React          | 19.2.0      |
| **CSS Framework**              | <img src="https://skillicons.dev/icons?i=tailwind" width="32" alt="Tailwind CSS"/>                                                                                 | Tailwind CSS   | 4.1.17      |
| **Build Tool**                 | <img src="https://skillicons.dev/icons?i=vite" width="32" alt="Vite"/>                                                                                             | Vite           | 7.2.2       |
| **Runtime Environment**        | <img src="https://skillicons.dev/icons?i=nodejs" width="32" alt="Node.js"/>                                                                                        | Node.js        | 22.12.0     |
| **Backend Framework**          | <img src="https://skillicons.dev/icons?i=express" width="32" alt="Express"/>                                                                                       | Express        | 5.1.0       |
| **Database**                   | <img src="https://skillicons.dev/icons?i=mongodb" width="32" alt="MongoDB"/>                                                                                       | MongoDB        | 8.0         |
| **Media Storage**              | <img src="https://raw.githubusercontent.com/tandpfun/skill-icons/231498caad5aa2ab9f05c4b6410fb5f7a8d3e424/icons/Cloudinary-Dark.svg" width="32" alt="Cloudinary"/> | Cloudinary     | 1.45.0      |
| **Authentication**             | <img src="https://img.icons8.com/?size=96&id=rHpveptSuwDz&format=png" width="32" alt="JWT"/>                                                                       | JWT            | 9.0.2       |
| **Mobile Experience**          | <img src="https://blog.openreplay.com/images/building-a-pwa-with-react/images/hero.png" width="32" alt="React+PWA"/>                                               | React PWA      | Manifest V3 |
| **Cloud Hosting**              | <img src="https://skillicons.dev/icons?i=aws" width="32" alt="AWS"/>                                                                                               | AWS            | Latest      |
| **Version Control**            | <img src="https://skillicons.dev/icons?i=github,githubactions" width="64" alt="GitHub"/>                                                                           | GitHub         | Latest      |

---

## **5. API Endpoints Reference**

### **I. Authentication Endpoints**

| **Endpoint**         | **Method** | **Description**               |
| -------------------- | ---------- | ----------------------------- |
| `/api/auth/register` | POST       | Create new user account       |
| `/api/auth/login`    | POST       | User login and JWT generation |
| `/api/auth/me`       | GET        | Get current user profile      |

### **II. Course Endpoints**

| **Endpoint**       | **Method** | **Description**                     |
| ------------------ | ---------- | ----------------------------------- |
| `/api/courses`     | GET        | Get all published courses (with search/filters)            |
| `/api/courses`     | POST       | Create new course (instructor only) |
| `/api/courses/:id` | GET        | Get specific course details                  |
| `/api/courses/:id` | PUT        | Update course (instructor only)     |
| `/api/courses/:id` | DELETE     | Delete course (instructor only)     |
| `/api/courses/instructor/:instructorId` | GET | Get instructor's courses |

### **III. Module Endpoints**

| **Endpoint**               | **Method** | **Description**      |
| -------------------------- | ---------- | -------------------- |
| `/api/modules/course/:courseId` | GET        | Get all modules for a course   |
| `/api/modules` | POST       | Create module (Instructor only) |
| `/api/modules/:id`         | DELETE     | Delete module (Instructor only)       |

### **IV. Enrollment Endpoints**

| **Endpoint**             | **Method** | **Description**             |
| ------------------------ | ---------- | --------------------------- |
| `/api/enrollments/course/:courseId`  | POST       | Enroll in course (Student only)            |
| `/api/enrollments/course/:courseId/status` | GET        | Check enrollment status |
| `/api/enrollments/course/:courseId` | GET | Get course enrollments (Instructor only) |
| `/api/enrollments/course/:courseId/complete` | PATCH | Mark course as completed (Student only) |

---

## **6. Conclusion**

**LearnX LMS** uses secure authentication and role-based authorization to provide:

- Clear separation of **Instructor** and **Student** views
- Safe and scalable system
- Ready for future features like progress tracking and payments
