# 🏛️ Scalable Social Media Backend (Django Architecture)

A robust, full-stack web application built using **Python** and the **Django Framework**. The project is designed using an enterprise-grade modular structure, separating business domains into isolated, reusable Django apps (`users` and `posts`) to maintain a clean separation of concerns and high scalability.

This system relies on the standard **Model-View-Template (MVT)** pattern to deliver secure authentication, dynamic data persistence, and cleanly decoupled URL routing.

---

## 🛠️ Project Architecture & Modular Apps

The application logic is decoupled into two primary internal subsystems to ensure high maintainability:

### 👤 1. The `users` Application
* **Responsibility:** Manages all identity operations, user safety, and account configurations.
* **Key Features:** User registration profiles, strict session management, secure password hashing, and user authentication mappings.

### 📝 2. The `posts` Application
* **Responsibility:** Dictates content management, creation workflows, and database entity relationships.
* **Key Features:** CRUD actions for posts, handling relational links (`ForeignKey` linking posts back to their specific user creators), and chronological feed queries.

---

## 📌 Application Routing Matrix

The project's routing system utilizes explicit URL inclusion (`include()`) to cleanly decouple application domains, alongside regular-expression pattern matching (`re_path`) to securely serve static and dynamic media assets.

| Route URL | Component / App | Description / Handled Functionality | Access Level |
| :--- | :--- | :--- | :--- |
| `/` | Core View | Core global homepage dashboard | Public |
| `/about/` | Core View | General application information and about page | Public |
| `/posts/*` | `posts.urls` | Subrouted content CRUD manager (Feed, Creation, Details) | App Dependent |
| `/users/*` | `users.urls` | Subrouted auth manager (Login, Registration, Profiles) | App Dependent |
| `/admin/` | Core Django | Advanced back-office database administrative control site | Staff / Admin |
| `/static/<path>` | Core Engine | Regular-expression route serving stylesheets, scripts, and fonts | Public |
| `/media/<path>` | Core Engine | Regular-expression route serving user-uploaded files and media assets | Public |

*Note: The project leverages Django's asset serving mechanisms mapped natively to `settings.STATIC_ROOT` and `settings.MEDIA_ROOT` via custom regular expression parameters to handle files dynamically during runtime.*

---

## 🏗️ Technical Highlights & Best Practices

* **Relational Database Design:** Implements a strict **One-to-Many relationship** (`ForeignKey`) between the `User` model and the `Post` model, ensuring database-level integrity so posts cannot exist without an owner.
* **Asset & Media Pipeline:** Configured custom regex routes to intercept traffic targeting assets, facilitating smooth processing of user avatar image uploads and site assets.
* **Defense-in-Depth Security:** Employs built-in protections against common web threats including Cross-Site Scripting (XSS), Cross-Site Request Forgery (CSRF tokens on all data submittals), and automated SQL Injections.

---

## ⚡ Setup and Local Installation

Follow these steps to configure and run the Django application locally:

1. **Clone the repository:**
   ```bash
   git clone https://github.com
   cd your-repo-name
   ```

2. **Set up a virtual environment:**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use: venv\Scripts\activate
   ```

3. **Install dependencies:**
   ```bash
   pip install django
   ```

4. **Run Database Migrations:**
   Apply global architectural updates and generate your relational schema tables:
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

5. **Create an Admin Account:**
   Generate credentials to verify database entries directly through the custom backend admin dashboard:
   ```bash
   python manage.py createsuperuser
   ```

6. **Boot up the server:**
   ```bash
   python manage.py runserver
   ```
   Open **`http://127.0.0`** to view the application homepage live, or visit **`http://127.0.0admin/`** to log into the administrative management console.
