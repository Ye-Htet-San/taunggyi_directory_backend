# Taunggyi Directory Backend 🏔️🔌

This is the high-performance REST API backend powering the **Taunggyi Directory** mobile application[cite: 1]. Built using modern Python frameworks, this server handles multi-role authentication, structured business directory lookups, user engagement architectures (reviews and reactions), and precise localized configurations[cite: 1].

---

## 🚀 Key Features

* **Advanced Authentication & RBAC:** Secure token-based OAuth2 system distributing JWT access and refresh tokens. Features Role-Based Access Control (RBAC) across three distinct tiers: `User`, `Owner`, and `Admin`.
* **Dynamic Location & Directory Core:** Supports complete CRUD capabilities for places, businesses, and sights. Tailored specifically for the local ecosystem, including specialized flags (`is_famous`, `is_popular`, `is_featured`) and native support for Myanmar Timezone configurations (UTC+06:30).
* **Granular Categorization:** Two-tier listing layout structured via main `Categories` and contextual `Subcategories` with administrative validation rules.
* **Interactive Community Review Engine:** Real-time user review engine with continuous place rating score aggregation and an internal tracking schema (`ReviewReaction`) to handle unique user likes/dislikes.
* **Asset Storage Pipeline:** Dedicated static image management engine routing isolated multi-part file uploads safely into localized application storage layers (`uploads/places` and `uploads/users`).
* **Database Evolution Tracking:** Database changes and schema updates are fully tracked and deployed smoothly using Alembic migrations.

---

## 🛠️ Tech Stack

* **Core Framework:** Python / [FastAPI](https://fastapi.tiangolo.com/) (Asynchronous high-performance design)
* **ORM & Database:** SQLAlchemy over SQLite Local Storage (`app.db`)
* **Database Migrations:** Alembic Migration Framework
* **Data Layer Validation:** Pydantic V2
* **Security & Cryptography:** Passlib (Bcrypt hashing) & Python-Jose (JWT Tokens execution)

---

## 📂 Project Structure

```text
├── ads/                  # Advertisement engine schemas, models, and routes
├── alembic/              # Database migration history and target environments
├── auth/                 # Authentication, profile logic, security dependencies
├── categories/           # Category data tier configurations
├── places/               # Base directory, flags, bookmarks, and coordinate rules
├── reviews/              # Review logic, score calculations, and reactions tracking
├── seeds/                # Initial startup data generation automation
├── subcategories/        # Sub-tier classification routing hooks
├── app.db                # Auto-generated relational SQLite database file
├── database.py           # Engine setup and Session context manager
└── main.py               # Main application initiation and CORS setup
```

---

## ⚙️ Getting Started

### Prerequisites

* Python 3.10+ installed on your system.

### Installation & Setup

1. **Clone the Repository:**
```bash
   git clone [https://github.com/Ye-Htet-San/taunggyi_directory_backend.git](https://github.com/Ye-Htet-San/taunggyi_directory_backend.git)
   cd taunggyi_directory_backend
   ```

2. **Initialize and Activate Virtual Environment:**
```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use: venv\Scripts\activate
   ```

3. **Install Dependencies:**
```bash
   pip install fastapi uvicorn sqlalchemy alembic pydantic passlib[bcrypt] python-jose python-multipart
   ```

4. **Execute Database Migrations:**
   Bring your local database schema completely up to date:
```bash
   alembic upgrade head
   ```

5. **Seed Initial Place Data:**
   Populate your local SQLite instance with seed directories:
```bash
   python -m seeds.seed_places
   ```

6. **Run the Application Server:**
```bash
   uvicorn main:app --host 0.0.0.0 --port 8000 --reload
   ```

Once fired up, the live server interface will be accessible locally via `http://localhost:8000`.

---

## 📖 API Documentation & Discovery

FastAPI generates clean, interactive documentation natively out of the box. While the backend server is running, you can explore, test, and view every underlying endpoint directly via your browser:

* **Interactive Swagger UI:** `http://localhost:8000/docs`
* **Alternative ReDoc UI:** `http://localhost:8000/redoc`

### Core API Endpoints Overview

| Tag | Base Endpoint | Description |
| :--- | :--- | :--- |
| **Auth** | `/auth` | Handles accounts registration, secure login, profile edits, password adjustments, and avatar tracking. |
| **Places** | `/places` | Location queries, user bookmark switches, and dedicated admin dashboard approval matrices. |
| **Categories** | `/categories` | Management for primary classification definitions. |
| **SubCategories** | `/subcategories` | Management for target secondary item matching pools. |
| **Reviews** | `/reviews` | Scoring calculations, review modification targets, and distinct user upvote/downvote operations. |