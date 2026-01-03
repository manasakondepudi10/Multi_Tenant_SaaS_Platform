# Multi-Tenant SaaS Platform

A fully containerized SaaS platform designed for multiple independent organizations to manage **users, projects, and tasks** securely within a single system.  
The platform ensures **strict tenant data isolation**, **JWT-based authentication (24h expiry)**, **RBAC authorization**, and **plan-based usage limits**, all initialized automatically through Docker.

---

## System Design Principles

- **Tenant-Scoped Data Access**: Queries are automatically filtered using trusted `tenant_id` from JWT claims.
- **Role-Validated API Operations**: All endpoints enforce RBAC at tenant or system level.
- **Automated Database Bootstrapping**: Schema setup, migrations, and seed data run on container startup.
- **Service Independence**: Frontend, backend, and database run as isolated containers for seamless development.

---

## Tech Stack

### Backend
- Node.js
- Express.js
- PostgreSQL 15
- JSON Web Token Authentication (24-hour expiry)
- Role-Based Access Control (RBAC)
- Tenant isolation middleware
- Audit logging for mutation events

### Frontend
- React (Vite)
- Axios for API communication
- UI adapts based on user roles and tenant scope

### Infrastructure
- Docker
- Docker Compose
- Automated SQL migrations via container entrypoint

---

## How to Run the Platform

### Prerequisites
Ensure installed:
- Docker
- Docker Compose

### Start the Application
From the **project root**, run:

```bash
docker-compose up -d --build
```
This will automatically:
- Launch PostgreSQL database
- Execute all migration files
- Seed sample tenant + user + project + task data
- Start backend API server
- Start frontend service
No manual database commands are required.

---

##  Access the Application

| Service      | URL                                                                  |
| ------------ | -------------------------------------------------------------------- |
| Frontend     | `http://localhost:3000`                      |
| Backend API  | `http://localhost:5000`                      |
| Health Check | `http://localhost:5000/api/health` |

---

## Supported Roles

- `super_admin` → System-level operations, tenant-agnostic access
- `tenant_admin` → Can manage users/projects/tasks within own organization only
- `user` → Regular tenant-scoped usage
All tenant-protected routes derive tenant_id from JWT, never from client input.

---

## API Features

- Tenant onboarding and authentication
- RBAC-validated user management
- Plan-restricted project creation
- Tenant-isolated task tracking
- Status updates for projects and tasks
- Audit logs recorded for CREATE/UPDATE/DELETE operations
- Middleware-enforced tenant boundary protection

---

## Testing the Platform

1. Open frontend in browser
2. Login using seeded credentials from submission.json
3. Validate:
   - Organization data isolation
   - Role-based access restrictions
   - Project and task CRUD operations
   - Plan usage limits

---

## Demo & Walkthrough

A system demonstration video covering:
   - Multi-tenant architecture
   - Docker container startup
   - Authentication flow
   - RBAC and isolation behavior
   - Project and task lifecycle

---

## Notes for Evaluators

- Platform is fully dockerized
- All services start using one command
- DB schema + migrations + seed run automatically
- No manual setup required
- Tenant isolation is enforced using JWT claims