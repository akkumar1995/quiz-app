# Quiz Management System

This canvas contains a full project plan (`PLAN.md`), repository layout, and key source files for a simple Quiz Management System using:

* Frontend: React (Create React App)
* Backend: Spring Boot (Gradle)
* Database: MySQL
* IDE: VSCode (UI) for frontend, IntelliJ for backend

> NOTE: This canvas contains the full `PLAN.md` and a set of representative source files and instructions. Use them as a complete starter project you can drop into a single GitHub repository.

---

## PLAN.md

### Project: Quiz Management System

**Date:** 2025-12-01

### 1) Assumptions

* Admin can create a quiz composed of questions. Each question can be of a supported type: `MCQ` (single correct option), `TRUE_FALSE`, or `TEXT` (free text answer).
* For `MCQ` and `TRUE_FALSE`, the system can automatically grade answers.
* For `TEXT`, the system performs a case-insensitive exact match to determine correctness (configurable in scope); otherwise consider manual review as a future improvement.
* No user accounts for public users; admin access is assumed to be done locally (no auth implemented in this MVP). Admin endpoints are REST endpoints.
* Single GitHub repository will contain two folders: `/backend` (Spring Boot) and `/frontend` (React).

### 2) Scope (MVP)

**Included**:

* Admin API to create quizzes with title and questions (MCQ/TF/Text).
* Public page to list or open a quiz by ID and take it.
* Auto-grading for MCQ and TRUE_FALSE; TEXT graded by exact match.
* Simple result display containing score and per-question correctness and correct answers.
* Persistence to MySQL with Spring Data JPA.
* React frontend with two pages: Admin Create Quiz and Public Take Quiz.
* `PLAN.md`, `README.md`, and instructions to run locally.

**Excluded (out of scope for MVP)**:

* Authentication/authorization for admin.
* Rich text editor for questions.
* Image, media or file uploads.
* Question-shuffling, timed quizzes, analytics, or grading policy variants.

### 3) Approach / Implementation plan

* Backend: Implement domain entities (Quiz, Question, Option, Submission, Answer). Expose REST endpoints:
   * POST /api/login - user login
   * POST ./api/signup - new user signup 
  * `POST /api/admin/quizzes` — create quiz (admin)
  * `GET /api/quizzes/{id}` — public fetch quiz (hide correct answers)
  * `POST /api/quizzes/{id}/submit` — submit answers, return results
* Frontend: React app with two routes:
	* /login and /signup 
  * `/admin` — form to build quiz and submit to admin API
  * `/quiz/:id` — fetch quiz JSON, render questions, submit answers, show results
* DB: MySQL — provide `application.properties` template (user must supply DB credentials). Use JPA/Hibernate with `ddl-auto=update` for convenience.
* One GitHub repo: `quiz-management-system/` with `backend/` and `frontend/`.

### 4) Scope changes during implementation (proposal)

* If the user wants authentication later, add JWT-based admin endpoints.
* If user wants manual grading for text answers, add an admin UI that shows ungraded submissions.

---