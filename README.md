<div align="center">

# 🎓 Internova
### University Internship & Industry Matching Portal

[![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](https://reactjs.org/)
[![.NET](https://img.shields.io/badge/.NET-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)](https://dotnet.microsoft.com/)
[![MySQL](https://img.shields.io/badge/MySQL-005C84?style=for-the-badge&logo=mysql&logoColor=white)](https://www.mysql.com/)
[![Azure](https://img.shields.io/badge/Microsoft_Azure-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)](https://github.com/features/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)

> **SE3022 – Case Study Project** | Year 3, BSc (Hons) in Computer Science

A full-stack web platform bridging the gap between students, companies, and university administrators — enabling seamless internship discovery, application tracking, project participation, and competition engagement.

</div>

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [System Architecture](#-system-architecture)
- [Tech Stack](#-tech-stack)
- [User Roles & Features](#-user-roles--features)
- [Internship Workflow](#-internship-workflow)
- [Database Design](#-database-design)
- [Repository Structure](#-repository-structure)
- [Getting Started](#-getting-started)
- [Testing Strategy](#-testing-strategy)
- [Deployment](#-deployment)
- [Agile Methodology](#-agile-methodology)
- [Security Features](#-security-features)
- [Future Enhancements](#-future-enhancements)
- [Expected Outcomes](#-expected-outcomes)
- [Team](#-team)
- [License](#-license)

---

## 🌐 Project Overview

**Internova** is a full-stack, cloud-deployed web application that serves as a centralised matching portal connecting:

| Stakeholder | Role |
|---|---|
| 🎓 **Students** | Discover internships, apply, track status, join projects & competitions |
| 🏢 **Companies** | Post verified internship listings, shortlist and schedule interviews |
| 🏛️ **University Admins** | Approve listings, manage ecosystem, generate reports |

The platform ensures **no student is left without opportunity** — those rejected from internships are seamlessly redirected through a continuity pipeline:

```
Internship Rejection → Project Participation → Startup Engagement → Competition Registration
```

---

## 🏗 System Architecture

Internova follows a **3-Tier Architecture** deployed on Microsoft Azure:

```
┌─────────────────────────────────────────────────────────────────┐
│                        CLIENT LAYER                             │
│                  React.js (Azure App Service)                   │
└──────────────────────────┬──────────────────────────────────────┘
                           │  HTTPS / REST API
┌──────────────────────────▼──────────────────────────────────────┐
│                     APPLICATION LAYER                           │
│            ASP.NET Core Web API (Azure App Service)             │
│         JWT Auth │ Role-Based Access │ Business Logic           │
└──────────┬───────────────────────────────────────┬─────────────┘
           │                                       │
┌──────────▼──────────┐                 ┌──────────▼──────────────┐
│     DATA LAYER      │                 │     FILE STORAGE        │
│  Azure Database     │                 │  Azure Blob Storage     │
│  for MySQL (3NF)    │                 │  (Resumes, Documents)   │
└─────────────────────┘                 └─────────────────────────┘
```

| Layer | Technology | Hosting |
|---|---|---|
| Presentation | React.js + Vite | Azure App Service |
| Application | ASP.NET Core Web API | Azure App Service |
| Data | MySQL | Azure Database for MySQL |
| File Storage | Azure Blob Storage | Azure Storage Account |

---

## ⚙️ Tech Stack

| Category | Technology |
|---|---|
| **Frontend** | React.js, Vite, React Router, Axios, Formik |
| **Backend** | ASP.NET Core Web API (.NET 8), Clean Architecture |
| **Database** | MySQL (Azure Database for MySQL Flexible Server) |
| **Cloud** | Microsoft Azure |
| **Storage** | Azure Blob Storage |
| **Authentication** | JWT Tokens + Role-Based Access Control (RBAC) |
| **Testing** | xUnit (Unit), Selenium (E2E), JMeter (Performance) |
| **CI/CD** | GitHub Actions / Azure DevOps Pipelines |
| **Version Control** | GitHub |

---

## 👥 User Roles & Features

### 🎓 Student Portal
- Register & login with role-based authentication
- Build and manage student profile
- Upload and store resume / documents
- Browse and search verified internship listings
- Submit internship applications and track status
- Apply for university project participation
- Discover and register for competitions & startup programmes

### 🏢 Company Portal
- Register and await admin verification
- Submit and manage internship listings
- Review and filter applicant profiles
- Accept or reject candidates with feedback
- Schedule interviews and manage slots

### 🏛️ Admin Portal
- Approve and verify company accounts
- Publish and manage internship listings
- Create and manage projects, competitions & startups
- Monitor platform analytics & generate reports
- Manage user accounts and roles

---

## 🔄 Internship Workflow

```
┌──────────┐    ┌────────────┐    ┌───────────┐    ┌──────────────────┐
│ Applied  │───▶│ Shortlisted│───▶│ Interview │───▶│ Selected 🎉      │
└──────────┘    └────────────┘    └───────────┘    └──────────────────┘
                                                           │
                                                     (If Rejected)
                                                           │
                                                           ▼
                                              ┌────────────────────────┐
                                              │  Project Participation │
                                              └───────────┬────────────┘
                                                          │
                                                          ▼
                                              ┌────────────────────────┐
                                              │   Startup Programme    │
                                              └───────────┬────────────┘
                                                          │
                                                          ▼
                                              ┌────────────────────────┐
                                              │  Competition Entry     │
                                              └────────────────────────┘
```

---

## 🗄 Database Design

The database is modelled in **Third Normal Form (3NF)** with enforced foreign key constraints, indexed lookup columns, and deployed on **Azure Database for MySQL Flexible Server**.

| Entity | Key Attributes |
|---|---|
| `User` | UserID, Email, PasswordHash, Role, CreatedAt |
| `StudentProfile` | StudentID, UserID (FK), GPA, CV_URL, Skills |
| `CompanyProfile` | CompanyID, UserID (FK), Industry, VerifiedAt |
| `Internship` | InternshipID, CompanyID (FK), Title, Deadline, Status |
| `InternshipApplication` | AppID, StudentID (FK), InternshipID (FK), Status |
| `Project` | ProjectID, Title, Description, Duration, MaxParticipants |
| `ProjectParticipation` | ParticipationID, StudentID (FK), ProjectID (FK), Status |
| `Competition` | CompetitionID, Title, RegistrationDeadline, PrizeInfo |
| `CompetitionParticipation` | EntryID, StudentID (FK), CompetitionID (FK), SubmissionURL |
| `DocumentStorage` | DocID, StudentID (FK), BlobURL, DocType, UploadedAt |

### Key Design Decisions
- **3NF Normalisation** — eliminating transitive dependencies across all entities
- **Foreign Key Constraints** — enforcing referential integrity at the DB level
- **Indexing** — on frequently queried columns (Email, Status, CompanyID, StudentID)
- **Soft Deletes** — `IsDeleted` flag to preserve audit history

---

## 📁 Repository Structure

```
Internova/
├── .github/
│   ├── workflows/          # CI/CD GitHub Actions pipelines
│   │   ├── frontend.yml
│   │   └── backend.yml
│   └── README.md           # ← You are here
│
├── internova-frontend/     # React.js Frontend (Vite)
│   ├── public/
│   ├── src/
│   │   ├── assets/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── services/       # Axios API service layer
│   │   ├── hooks/
│   │   ├── context/
│   │   └── utils/
│   ├── .env.example
│   └── package.json
│
├── internova-backend/      # ASP.NET Core Web API (Clean Arch.)
│   ├── Internova.Api/      # Presentation layer (Controllers)
│   ├── Internova.Core/     # Domain entities & interfaces
│   ├── Internova.Infrastructure/ # EF Core, Repos, Azure services
│   └── Internova.Tests/    # Unit & integration tests
│
├── database/
│   ├── schema.sql          # DDL scripts
│   ├── seed.sql            # Sample data
│   └── migrations/
│
├── docs/
│   ├── SRS.pdf
│   ├── DesignDocument.pdf
│   └── diagrams/
│
└── tests/
    ├── selenium/           # End-to-end UI tests
    └── jmeter/             # Performance test plans
```

---

## 🚀 Getting Started

### Prerequisites

| Requirement | Version |
|---|---|
| Node.js | ≥ 18.x |
| .NET SDK | 8.0 |
| MySQL Server | 8.x |
| Azure CLI (optional) | Latest |

### 1. Clone the Repository

```bash
git clone https://github.com/<org>/Internova.git
cd Internova
```

### 2. Frontend Setup

```bash
cd internova-frontend
cp .env.example .env          # Configure API base URL
npm install
npm run dev
```

### 3. Backend Setup

```bash
cd internova-backend
cp Internova.Api/appsettings.example.json Internova.Api/appsettings.json
# Fill in DB connection string, JWT secret, Azure Blob config
dotnet restore
dotnet run --project Internova.Api/Internova.Api.csproj
```

### 4. Database Setup

```bash
mysql -u root -p < database/schema.sql
mysql -u root -p internova_db < database/seed.sql
```

> **Swagger UI** is available at `https://localhost:<port>/swagger` in development mode.

---

## 🧪 Testing Strategy

| Test Type | Tool / Framework | Coverage Target |
|---|---|---|
| Unit Testing | xUnit (.NET) / Jest (React) | ≥ 80% |
| Integration Testing | xUnit + TestContainers | API + DB flows |
| System Testing | Manual + Selenium | End-to-end user journeys |
| Performance Testing | Apache JMeter | 100+ concurrent users |
| Security Testing | OWASP ZAP / Manual | Auth, SQL injection |
| Regression Testing | GitHub Actions (on push) | All critical paths |
| User Acceptance Testing | Stakeholder walkthroughs | Sprint reviews |

### Sample Test Cases

| TC ID | Feature | Input | Expected Output | Status |
|---|---|---|---|---|
| TC-001 | Student Login | Valid credentials | JWT returned, redirect to dashboard | ✅ Pass |
| TC-002 | Student Login | Invalid password | 401 Unauthorized | ✅ Pass |
| TC-003 | Internship Apply | Authenticated student | Application saved, status = "Applied" | ✅ Pass |
| TC-004 | Company Verify | Unverified company adds listing | 403 Forbidden | ✅ Pass |
| TC-005 | Document Upload | PDF ≤ 5 MB | Blob URL stored, 200 OK | ✅ Pass |
| TC-006 | Admin Approve | Admin approves company | Company status = "Verified" | ✅ Pass |

---

## ☁️ Deployment

All services are hosted on **Microsoft Azure**:

```
┌──────────────────────────────────────────────────────────────────┐
│                       Microsoft Azure                            │
│                                                                  │
│  ┌─────────────────────┐     ┌─────────────────────────────┐    │
│  │  Azure App Service  │     │     Azure App Service       │    │
│  │   (Frontend)        │────▶│       (Backend API)         │    │
│  │   React / Vite      │     │   ASP.NET Core Web API      │    │
│  └─────────────────────┘     └──────────────┬──────────────┘    │
│                                             │                   │
│                          ┌──────────────────┴───────────────┐   │
│                          │                                   │   │
│              ┌───────────▼───────────┐  ┌───────────────────▼─┐ │
│              │  Azure Database for   │  │  Azure Blob Storage │ │
│              │  MySQL (Flexible)     │  │  (Documents, CVs)   │ │
│              └───────────────────────┘  └─────────────────────┘ │
└──────────────────────────────────────────────────────────────────┘
```

### Deployment Checklist

- [x] HTTPS enforced via Azure-managed SSL certificates
- [x] Environment variables configured via Azure App Service Configuration
- [x] Database connection secured with private networking
- [x] Azure Blob Storage access via SAS tokens (no public anonymous access)
- [x] CI/CD pipeline configured with **GitHub Actions**
- [x] Automated deployments triggered on merge to `main`

### CI/CD Pipeline Overview

```yaml
# On push to main:
1. Run unit tests (xUnit / Jest)
2. Build frontend (npm run build)
3. Build backend (dotnet publish)
4. Deploy frontend → Azure App Service
5. Deploy backend  → Azure App Service
6. Run smoke tests
```

---

## 📊 Agile Methodology

The project follows **Scrum / Agile** over a **16-week development cycle**:

| Sprint | Duration | Focus |
|---|---|---|
| Sprint 1–2 | Weeks 1–4 | Requirements, SRS, Architecture Design |
| Sprint 3–5 | Weeks 5–8 | Core Auth, Student & Company Portals |
| Sprint 6–9 | Weeks 9–12 | Admin Portal, Workflow Engine, File Upload |
| Sprint 10–12 | Weeks 13–16 | Testing, Deployment, Documentation |

### Team Practices
- 📅 **Daily Standups** — 15-minute syncs (What I did / What I'll do / Blockers)
- 🔁 **Sprint Reviews** — Demo to academic supervisor at the end of each sprint
- 💬 **Retrospectives** — Team reflection on process improvement
- 🔄 **Role Rotation** — BA → Developer → QA → DevOps, rotating per sprint
- 📋 **Jira Backlog Grooming** — Weekly backlog refinement with story points

---

## 🔒 Security Features

| Feature | Implementation |
|---|---|
| **HTTPS** | Enforced at Azure App Service level |
| **Authentication** | JWT Bearer tokens with expiry |
| **Authorisation** | Role-Based Access Control (Student / Company / Admin) |
| **Input Validation** | Server-side with FluentValidation, client-side with Formik |
| **SQL Injection Prevention** | EF Core parameterised queries (no raw SQL) |
| **File Upload Safety** | MIME-type validation, size limits, malware policy |
| **Blob Storage Security** | SAS token-based access (no public endpoints) |
| **CORS Policy** | Restricted origin allowlist |

---

## 📈 Future Enhancements

- 🤖 **AI-Based Internship Recommendation** — ML model matching student skills to listings
- 📄 **Resume Scoring Engine** — NLP-driven CV quality scoring
- 🔍 **Skill Gap Analysis** — Personalised upskilling recommendations
- 📊 **Analytics Dashboard** — Platform-wide KPIs for admin insight
- 🚀 **Startup Incubation Tracking** — Milestone-based progress monitoring
- 📲 **Mobile App** — React Native companion app
- 🌐 **Multi-Institution Support** — Expand beyond a single university

---

## 🎯 Expected Outcomes

| Outcome | Description |
|---|---|
| ✅ Verified Access | Students access only approved, validated internship listings |
| 📊 Transparent Workflow | End-to-end visibility of application stages for all stakeholders |
| 🎓 Improved Employability | Structured pathway from internships → projects → competitions |
| 🤝 Stronger Collaboration | Direct, accountable channel between university and industry |

---

## 👨‍💻 Team

> SE3022 Case Study Project — Year 3, Group [Group ID]

| Name | Role | GitHub |
|---|---|---|
| Janeesha Gamage | Full-Stack Developer / BA | [@J4N3i](https://github.com/J4N3i) |
| Member 2 | Backend Developer / DevOps | [@username](https://github.com) |
| Member 3 | Frontend Developer / QA | [@username](https://github.com) |
| Member 4 | Database Engineer / QA | [@username](https://github.com) |

> **Academic Supervisor:** [Supervisor Name], Department of Computer Science

---

## 📜 License

This project is licensed under the **MIT License** — see the [LICENSE](../LICENSE) file for full details.

```
MIT License — Copyright (c) 2026 Internova Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...
```

---

<div align="center">

**Developed as part of SE3022 – Case Study Project, Year 3, BSc (Hons) in Computer Science.**

*Department of Computer Science & Engineering | 2025–2026*

</div>