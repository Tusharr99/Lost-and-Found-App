# 🔍 Lost & Found Campus Portal

A modern, full-stack web application designed for campus communities to streamline reporting, browsing, and reclaiming lost and found items.

---

## 🚀 Tech Stack

### Backend
- **Framework:** Spring Boot 3.5.6 (Java 17/20)
- **Security:** Spring Security + Stateless JWT Authentication (JJWT 0.11.5)
- **Password Hashing:** BCrypt (`BCryptPasswordEncoder`)
- **ORM / Persistence:** Spring Data JPA (Hibernate 6)
- **Database:** MySQL 8
- **Build Tool:** Maven Wrapper (`mvnw`)

### Frontend
- **Framework:** React 19 + Vite 7
- **Styling:** Tailwind CSS v4 (`@tailwindcss/vite`)
- **Routing:** React Router v7 (`react-router-dom`)
- **Icons:** Lucide React
- **HTTP Client:** Axios (with automatic Bearer token interceptor)
- **Media Hosting:** Cloudinary (direct client upload)

---

## ✨ Features

- 🔐 **Authentication & Authorization:** Secure registration and login with JWT tokens and role-based access control (`ROLE_USER`, `ROLE_ADMIN`).
- 📢 **Post Lost or Found Items:** Report items with title, detailed description, category, location, timestamp, contact details, and images.
- 🖼️ **Image Upload:** Upload item photos directly to Cloudinary storage.
- 🔎 **Real-time Search & Filter:** Filter items by category (Electronics, Documents, Keys, Wallets, Other) and status (`OPEN`, `RESOLVED`), with client-side keyword search.
- ✉️ **Contact Finder/Owner:** One-click email connection (`mailto:`) to facilitate quick returns.
- 📌 **My Posted Items:** Dedicated dashboard to view, edit, or delete items posted by the logged-in user.
- 🛡️ **Admin Dashboard:** Administrative panel to view all users, promote users to Admin, or delete user accounts.

---

## 📁 Project Structure

```
Lost-and-Found-App-main/
├── backend/
│   ├── src/main/java/com/lostfound/
│   │   ├── config/          # Security, JWT, CORS, Cloudinary, and Password configs
│   │   ├── controller/      # REST APIs (/api/auth, /api/items, /api/users)
│   │   ├── dto/             # Request & Response Data Transfer Objects
│   │   ├── mapper/          # Entity <-> DTO mappers
│   │   ├── model/           # JPA Entities (Item, User)
│   │   ├── repository/      # Spring Data JPA repositories
│   │   └── service/         # Business logic layer
│   ├── src/main/resources/
│   │   └── application.properties # Server, database, and JWT configs
│   ├── Dockerfile
│   ├── mvnw & mvnw.cmd
│   └── pom.xml
│
├── frontend/
│   ├── src/
│   │   ├── api/             # Modular API service calls
│   │   ├── components/      # Reusable components (Navbar, ItemCard, Route Guards)
│   │   ├── context/         # AuthContext
│   │   ├── pages/           # Pages (Hero, Login, Register, Lost, Found, Add, Admin)
│   │   ├── App.jsx
│   │   └── axiosConfig.js
│   ├── package.json
│   └── vite.config.js
└── README.md
```

---

## 🛠️ Getting Started

### Prerequisites
- **Java JDK 17+** (JDK 17, 20, or 21)
- **Node.js 18+** & npm
- **MySQL 8.x** (or XAMPP)

---

### 1. Database Setup
1. Start your local MySQL server (port `3306`).
2. Verify or create the database:
   ```sql
   CREATE DATABASE IF NOT EXISTS lostfound_db;
   ```
3. Update database credentials in `backend/src/main/resources/application.properties` if needed:
   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/lostfound_db?createDatabaseIfNotExist=true
   spring.datasource.username=root
   spring.datasource.password=YOUR_MYSQL_PASSWORD
   ```

---

### 2. Backend Setup
1. Open terminal and navigate to `backend`:
   ```bash
   cd backend
   ```
2. Run Spring Boot:
   - **Windows:**
     ```powershell
     .\mvnw.cmd spring-boot:run
     ```
   - **Linux / macOS:**
     ```bash
     chmod +x mvnw
     ./mvnw spring-boot:run
     ```
   The backend will be running at `http://localhost:8080`.

---

### 3. Frontend Setup
1. In a separate terminal, navigate to `frontend`:
   ```bash
   cd frontend
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Start the development server:
   ```bash
   npm run dev
   ```
   The frontend will be running at `http://localhost:5173`.

> **Note:** To point the frontend to your local backend, ensure `baseURL: "http://localhost:8080/api"` is set in `frontend/src/axiosConfig.js`.

---

## 📡 API Endpoints

### Auth (`/api/auth`)
| Method | Endpoint | Description | Access |
|---|---|---|---|
| `POST` | `/api/auth/register` | Register a new user | Public |
| `POST` | `/api/auth/login` | Login and obtain JWT token | Public |

### Items (`/api/items`)
| Method | Endpoint | Description | Access |
|---|---|---|---|
| `GET` | `/api/items` | Get all items (filters: `type`, `status`, `category`) | User / Admin |
| `GET` | `/api/items/{id}` | Get item by ID | User / Admin |
| `POST` | `/api/items` | Create new item | User / Admin |
| `PUT` | `/api/items/{id}` | Update item (owner or admin) | User / Admin |
| `DELETE` | `/api/items/{id}` | Delete item (owner or admin) | User / Admin |
| `GET` | `/api/items/my-items` | Get current user's items | User / Admin |
| `PUT` | `/api/items/{id}/resolve`| Mark item as resolved | Owner / Admin |

### Users (`/api/users`)
| Method | Endpoint | Description | Access |
|---|---|---|---|
| `GET` | `/api/users` | List all registered users | Admin |
| `GET` | `/api/users/{id}` | Get user by ID | Admin |
| `PUT` | `/api/users/{id}` | Update user details | Admin |
| `POST` | `/api/users/{id}/make-admin` | Promote user to admin | Admin |
| `DELETE` | `/api/users/{id}` | Delete user | Admin |

---

## 📄 License
This project is open source and available under the [MIT License](LICENSE).
