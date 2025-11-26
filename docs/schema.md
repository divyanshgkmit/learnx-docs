# **LearnX LMS - Database Schema**

## **1. Overview**

This schema defines the core data structure for **LearnX LMS**, including **Users, Roles, Courses, Modules, and Enrollments**.
It ensures relational integrity and supports the platform's main functionalities: authentication, course creation, media management, and enrollment tracking.

## **2. ER Diagram**

![logo](assets/mermaid.png)

---

## **3. Collection Details**

| Collection | Fields | Notes / Purpose |
|------------|--------|-----------------|
| **USERS** | `_id`, `fullName`, `email`, `password`, `timestamps` | User accounts with authentication |
| **ROLES** | `_id`, `name`, `timestamps` | User roles (Instructor/Student) |
| **USER_ROLES** | `_id`, `userId`, `roleId`, `timestamps` | Links users with roles |
| **COURSES** | `_id`, `instructorId`, `title`, `category`, `difficultyLevel`, `description`, `thumbnailUrl`, `price`, `isPublished`, `timestamps` | Course details with media |
| **MODULES** | `_id`, `courseId`, `title`, `videoUrl`, `duration`, `order`, `timestamps` | Course lessons with videos |
| **ENROLLMENTS** | `_id`, `studentId`, `courseId`, `amountPaid`, `isCompleted`, `timestamps` | Student enrollments with progress |

---

## **4. Indexing**

| Collection | Field(s) | Purpose |
|------------|----------|---------|
| **USERS** | `email` | Unique login and user search |
| **USER_ROLES** | `userId`, `roleId` | Prevent duplicate roles |
| **COURSES** | `instructorId` | Fetch instructor courses |
| **COURSES** | `isPublished` | Filter published courses |
| **MODULES** | `courseId`, `order` | Maintain module sequence |
| **ENROLLMENTS** | `studentId`, `courseId` | Prevent duplicate enrollments |

---

## **5. Relationships**

* **Users ↔ Roles**: Many-to-many via `USER_ROLES`
* **Instructor → Courses**: One-to-many
* **Course → Modules**: One-to-many  
* **Students ↔ Courses**: Many-to-many via `ENROLLMENTS`