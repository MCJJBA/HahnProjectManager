# Task Manager Application

A full-stack task management application built with **Spring Boot** (backend) and **React** (frontend).

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|------------|
| **Backend** | Java 11, Spring Boot 2.7.18, Spring Security, JWT |
| **Frontend** | React 18, React Router, Axios |
| **Database** | MySQL |
| **Build Tool** | Maven |

---

## 📁 Project Structure

```
taskproject/
├── backend/                 # Spring Boot REST API
│   ├── src/main/java/com/taskmanager/
│   │   ├── controller/      # REST endpoints
│   │   ├── service/         # Business logic
│   │   ├── repository/      # Database access
│   │   ├── model/           # Entity classes (User, Project, Task)
│   │   ├── dto/             # Data Transfer Objects
│   │   ├── security/        # JWT authentication
│   │   └── config/          # App configuration
│   └── pom.xml
│
└── frontend/                # React application
    ├── src/
    │   ├── components/      # Reusable components (Navbar)
    │   ├── pages/           # Page components (Login, Projects, etc.)
    │   ├── context/         # React Context (AuthContext)
    │   └── services/        # API service (Axios)
    └── package.json
```

---

## 🚀 How to Start the Application

### Prerequisites
- **Java 11** installed
- **Node.js** (v16+) installed
- **MySQL** running with database `task_manager` created

### 1. Setup MySQL Database

```sql
CREATE DATABASE task_manager;
```

### 2. Start Backend (Port 8082)

```powershell
cd backend
.\mvnw.cmd spring-boot:run
```

The backend will start at: `http://localhost:8082`

### 3. Start Frontend (Port 3000)

```powershell
cd frontend
npm install    # First time only
npm start
```

The frontend will start at: `http://localhost:3000`

---

## 🔐 Authentication

The app uses **JWT (JSON Web Token)** authentication.

### Test User Credentials
| Email | Password |
|-------|----------|
| `test@example.com` | `password123` |

### Auth Flow
1. User registers or logs in via `/api/auth/register` or `/api/auth/login`
2. Server returns a JWT token
3. Token is stored in localStorage
4. All subsequent requests include the token in the `Authorization` header

---

## 📡 API Endpoints

### Authentication
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Register new user |
| POST | `/api/auth/login` | Login and get JWT token |

### Projects
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/projects` | Get all user's projects |
| GET | `/api/projects/{id}` | Get project by ID |
| POST | `/api/projects` | Create new project |
| PUT | `/api/projects/{id}` | Update project |
| DELETE | `/api/projects/{id}` | Delete project |

### Tasks
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/projects/{projectId}/tasks` | Get all tasks in project |
| POST | `/api/projects/{projectId}/tasks` | Create new task |
| PUT | `/api/projects/{projectId}/tasks/{taskId}` | Update task |
| PATCH | `/api/projects/{projectId}/tasks/{taskId}/toggle` | Toggle task completion |
| DELETE | `/api/projects/{projectId}/tasks/{taskId}` | Delete task |
| GET | `/api/projects/{projectId}/progress` | Get project progress |

---

## ✨ Features

- ✅ User registration and login
- ✅ Create, edit, and delete projects
- ✅ Add tasks to projects
- ✅ Mark tasks as complete/incomplete
- ✅ View project progress (percentage of completed tasks)
- ✅ JWT-based secure authentication
- ✅ Responsive UI

---

## ⚙️ Configuration

### Backend (`backend/src/main/resources/application.properties`)

```properties
server.port=8082
spring.datasource.url=jdbc:mysql://localhost:3306/task_manager
spring.datasource.username=root
spring.datasource.password=Root12345@
jwt.secret=your-secret-key
jwt.expiration=86400000
```

### Frontend API Base URL (`frontend/src/services/api.js`)

```javascript
baseURL: 'http://localhost:8082/api'
```

---

## 🗄️ Database Schema

### Users Table
| Column | Type |
|--------|------|
| id | BIGINT (PK) |
| name | VARCHAR(100) |
| email | VARCHAR(255) UNIQUE |
| password | VARCHAR(255) |

### Projects Table
| Column | Type |
|--------|------|
| id | BIGINT (PK) |
| title | VARCHAR(200) |
| description | VARCHAR(1000) |
| user_id | BIGINT (FK) |
| created_at | DATETIME |
| updated_at | DATETIME |

### Tasks Table
| Column | Type |
|--------|------|
| id | BIGINT (PK) |
| title | VARCHAR(200) |
| description | VARCHAR(1000) |
| completed | BOOLEAN |
| due_date | DATE |
| project_id | BIGINT (FK) |
| created_at | DATETIME |
| updated_at | DATETIME |

---

## 🧪 Quick Test

1. Start both backend and frontend
2. Open `http://localhost:3000`
3. Login with `test@example.com` / `password123`
4. Create a new project
5. Add tasks to the project
6. Toggle tasks as complete
7. View progress bar update

---

## 📝 Notes

- The backend automatically creates database tables on startup
- A test user is created automatically if it doesn't exist
- JWT tokens expire after 24 hours
- CORS is configured to allow requests from `http://localhost:3000`
