<div align="center">

# 🎓 Student Data Verification System (SVS)

**A full-stack web portal for university-level student data verification and management**

[![Live Demo](https://img.shields.io/badge/🚀%20Live%20Demo-Vercel-black?style=for-the-badge&logo=vercel)](https://student-management-portal.vercel.app)
[![GitHub](https://img.shields.io/badge/GitHub-Repository-181717?style=for-the-badge&logo=github)](https://github.com/shreyay1310-svg/student-management-portal)
[![React](https://img.shields.io/badge/React-19-61DAFB?style=for-the-badge&logo=react)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.9-3178C6?style=for-the-badge&logo=typescript)](https://www.typescriptlang.org)
[![Hono](https://img.shields.io/badge/Hono-4.8-E36002?style=for-the-badge&logo=hono)](https://hono.dev)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?style=for-the-badge&logo=mysql)](https://mysql.com)

</div>

---

## 📌 Overview

The **Student Data Verification System (SVS)** is a multi-role, multi-tenant ERP web portal designed for universities and affiliated colleges to manage and verify student data digitally. It streamlines the entire student data submission lifecycle — from initial registration to document upload, staff verification, and final approval.

The system supports **bilingual data entry (English & Hindi)**, role-based access control, OTP-based authentication, and document management (photo, marksheet, signature, application letter).

---

## 🌐 Live Demo

> **🔗 [https://student-management-portal.vercel.app](https://student-management-portal.vercel.app)**

### Demo Credentials

| Role | User ID | Password |
|------|---------|----------|
| 🛡️ Admin | `ADMIN001` | `Rahul@8052` |
| 🎓 Student | Roll No: `123465` | `Rahil@8052` |

---

## ✨ Features

### 👨‍💼 Admin & Staff Panel
- **Dashboard** — Live stats for colleges, courses, subjects, students, and final submissions
- **University Management** — Multi-tenant university setup
- **College Management** — Manage affiliated colleges with full details (accreditation, principal, contacts)
- **Course & Subject Management** — Add courses (Honours/Masters) and link subjects with marks, credits, lab requirements
- **Student Management** — View, verify, approve, or reject student records with reasons
- **User Management** — Create and manage staff/admin accounts with role-based access
- **Role Management** — Custom roles with granular permissions
- **Reports** — Filterable student reports with category and gender stats; export to Excel/PDF
- **Activity Logs** — Full audit trail of all user actions

### 🎓 Student Portal
- **Self-Registration** — Students fill in personal, academic, and family details
- **Document Upload** — Photo, marksheet, application letter, and digital signature
- **Bilingual Form** — Fields for both English and Hindi names
- **Final Submission** — OTP-verified final submit with lock mechanism
- **Re-edit Requests** — Admins can unlock forms for corrections

### 🔐 Authentication & Security
- JWT-based session management
- OTP verification via email/mobile for critical actions
- Password hashing with bcryptjs
- Role-based route protection (Admin / Staff / Student)

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | React 19, TypeScript, Vite 7, Tailwind CSS v3, shadcn/ui |
| **Backend** | Hono 4 (Node.js), tRPC v11 |
| **Database** | MySQL 8 via Drizzle ORM |
| **Auth** | JWT (jose), bcryptjs, OTP via Nodemailer |
| **State Management** | TanStack Query v5, React Hook Form, Zod |
| **Charts & Export** | Recharts, jsPDF, xlsx |
| **Launcher** | .NET C# Windows launcher (`.exe`) |
| **Deployment** | Vercel (Frontend + API) |

---

## 🗄️ Database Schema

The system uses a **multi-tenant MySQL** schema with the following core tables:

```
universities  ──< colleges  ──< courses  ──< subjects
                     │
                     └──< students ──> users
                                │
                                └── activity_logs
                                └── otp_records
                                └── roles
```

| Table | Description |
|-------|-------------|
| `universities` | Top-level multi-tenant entity |
| `colleges` | Affiliated colleges under a university |
| `courses` | Courses offered by a college (BA, MA, etc.) |
| `subjects` | Subjects mapped to courses (Honours/Masters) |
| `students` | Student records with document URLs and verification status |
| `users` | System users — Admin, Staff, Student |
| `roles` | Custom permission-based roles |
| `otp_records` | OTP audit log for login/submit/registration |
| `activity_logs` | Full system audit trail |

---

## 🚀 Getting Started

### Prerequisites

- Node.js 20+
- MySQL 8.0+
- pnpm (or npm)

### 1. Clone the Repository

```bash
git clone https://github.com/shreyay1310-svg/student-management-portal.git
cd student-management-portal/app
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment Variables

Copy the example env file and fill in your values:

```bash
cp .env.example .env
```

```env
# Backend
APP_ID=your_app_id
APP_SECRET=your_jwt_secret

# Database
DATABASE_URL=mysql://user:password@localhost:3306/svs_db

# Frontend (Vite)
VITE_KIMI_AUTH_URL=https://auth.example.com
VITE_APP_ID=your_app_id

# Backend Auth
KIMI_AUTH_URL=https://auth.example.com
KIMI_OPEN_URL=https://open.example.com

# Admin
OWNER_UNION_ID=your_admin_union_id
```

### 4. Setup the Database

```bash
# Run migrations
npm run db:push

# (Optional) Seed with demo data
# Visit: http://localhost:3000/api/seed
```

### 5. Run Development Server

```bash
npm run dev
```

App will be available at **http://localhost:5173** (frontend) and **http://localhost:3000** (API).

### 6. Build for Production

```bash
npm run build
npm run start
```

---

## 📁 Project Structure

```
svs/
├── app/                        # Main application
│   ├── api/                    # Backend (Hono + tRPC routers)
│   │   ├── boot.ts             # Server entry point
│   │   ├── router.ts           # Root tRPC router
│   │   ├── auth-router.ts      # Authentication routes
│   │   ├── student-router.ts   # Student CRUD & verification
│   │   ├── college-router.ts   # College management
│   │   ├── course-router.ts    # Course management
│   │   ├── subject-router.ts   # Subject management
│   │   ├── university-router.ts# University management
│   │   ├── user-router.ts      # User management
│   │   ├── role-router.ts      # Role & permissions
│   │   ├── report-router.ts    # Reports & dashboard stats
│   │   ├── activity-router.ts  # Audit logs
│   │   └── otp-router.ts       # OTP send/verify
│   ├── db/
│   │   └── schema.ts           # Drizzle ORM schema (all tables)
│   ├── src/
│   │   ├── pages/              # React page components
│   │   │   ├── Dashboard.tsx
│   │   │   ├── StudentForm.tsx
│   │   │   ├── StudentManagement.tsx
│   │   │   ├── CollegeManagement.tsx
│   │   │   ├── CourseManagement.tsx
│   │   │   ├── SubjectManagement.tsx
│   │   │   ├── UniversityManagement.tsx
│   │   │   ├── UserManagement.tsx
│   │   │   ├── RoleManagement.tsx
│   │   │   ├── Reports.tsx
│   │   │   ├── ActivityLogs.tsx
│   │   │   └── Login.tsx
│   │   ├── components/         # Reusable UI components (shadcn/ui)
│   │   ├── hooks/              # Custom React hooks
│   │   ├── providers/          # Context providers
│   │   └── App.tsx             # Root component & routing
│   ├── contracts/              # Shared tRPC types
│   ├── scripts/                # DB seed & utility scripts
│   ├── Dockerfile              # Docker configuration
│   ├── docker-compose.yml      # Docker Compose (app + MySQL)
│   └── drizzle.config.ts       # Drizzle ORM config
├── launcher/
│   └── Program.cs              # .NET C# Windows launcher
├── Start-App.bat               # Quick-start batch file (Windows)
└── StudentDataVerification.exe # Packaged Windows launcher
```

---

## 🐳 Docker Setup

Run the full stack (app + MySQL) with Docker:

```bash
cd app
docker-compose up --build
```

---

## 📜 Available Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start dev server (Vite + Hono) |
| `npm run build` | Build frontend + bundle API |
| `npm run start` | Start production server |
| `npm run lint` | ESLint check |
| `npm run format` | Prettier formatting |
| `npm run test` | Run Vitest tests |
| `npm run db:generate` | Generate Drizzle migrations |
| `npm run db:migrate` | Apply migrations |
| `npm run db:push` | Push schema to DB (dev) |

---

## 🪟 Windows Launcher

For Windows users, a packaged `.exe` launcher is provided at the root:

```
StudentDataVerification.exe
```

Or simply run:

```
Start-App.bat
```

This automatically starts the Node.js server and opens the app in your default browser.

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Commit your changes: `git commit -m 'Add some feature'`
4. Push to the branch: `git push origin feature/my-feature`
5. Open a Pull Request

---

## 📄 License

This project is licensed under the **MIT License**.

---

<div align="center">

Made with ❤️ for digital education management

**[Live Demo](https://student-management-portal.vercel.app)** • **[GitHub](https://github.com/shreyay1310-svg/student-management-portal)**

</div>

