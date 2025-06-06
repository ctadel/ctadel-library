# ctadel Web Library

The **ctadel Web Library** is a web-based document management and conversational query system. It allows users to upload documents, manage them via a role-based dashboard, and query them through a backend-managed ingestion and retrieval service.

This monorepo includes the backend / frontend application (as a submodule), deployment configurations, and infrastructure provisioning files.

---

## Repository Structure

| Path | Description |
|------|-------------|
| `/backend` [Git Submodule] | Python FastAPI service for authentication, document ingestion, retrieval, and chat-based querying. |
| `/frontend` [Git Submodule] | Angular-based web application for user interaction, document upload, search, and dashboard management. |
| [`/k8s`](./k8s) | Kubernetes deployment manifests for backend, frontend, and PostgreSQL services. |
| [`/docker-compose.yaml`](./docker-compose.yaml) | Docker Compose configuration for local development and testing.

---

## Key Features

- **Document Upload & Management** (PDF, TXT, DOCX)
- **Role-Based Access Control**
  - Guest: Explore public documents
  - Basic User: Query unlimited but limited ingestions (3 max)
  - Premium User: Unlimited ingestions and query
- **Query Interface** for document conversation
- **View and Star Tracking**
- **Admin Dashboard** for managing users and documents

---

## Technology Stack

- **Backend**: FastAPI, SQLAlchemy (async), PostgreSQL, Alembic, Uvicorn, Pytest
- **Frontend**: Angular, SCSS, Tailwind CSS, NGINX
- **Auth**: JWT-based with role control
- **Database**: PostgreSQL
- **Containerization**: Docker, Docker Compose
- **Deployment**: Kubernetes (YAML-based), compatible with Helm

---

## Getting Started (Local Development)

### Prerequisites

- Docker + Docker Compose

### 1. Clone Repository

```bash
git clone https://github.com/ctadel/ctadel-web-library.git
cd ctadel-library
```

### 2. Configure Environment

```bash
cp backend/.env.sample backend/.env
# Edit the .env file to include required values like database URL and secrets.
```

### 3. Start Application

```bash
docker-compose up --build
```

This docker-compose uses the following services:
 - Backend (FastAPI)
 - Frontend (Angular)
 - PostgreSQL (Database)
 - Python script (Faker) to create some activity for quick demo

 Demo users and documents will be created automatically.
 Run docker-compose and start using the service as if it is already in production.
 Login with the following credentials:
    - For Basic User: `baisc: password`
    - For Premium User: `premium: password`
    - For Admin User: `moderator: password`


### 4. Access Services

- Frontend: [http://localhost:4200](http://localhost:4200)
- Backend API: [http://localhost:8000/docs](http://localhost:8000/docs)
- PostgreSQL: `localhost:15432`

---

## Apply Migrations

If needed, apply Alembic migrations:
(*already a part of docker-compose file*)

```bash
docker-compose run --rm cl_backend alembic upgrade head
```

---

## Kubernetes Deployment

The platform can be deployed using the provided Kubernetes manifests.

### Deploy Steps

1. Namespace:
   ```bash
   kubectl apply -f k8s/namespace.yaml
   ```

2. PostgreSQL:
   ```bash
   kubectl apply -f k8s/postgres.yaml
   ```

3. Backend:
   ```bash
   kubectl apply -f k8s/backend.yaml
   ```

4. Frontend:
   ```bash
   kubectl apply -f k8s/frontend.yaml
   ```

Update image tags and environment variables as required per cluster/environment.

---

## Github Sub-Repositories

- Library Backend (FastAPI)- [wlib-backend](https://github.com/ctadel/wlib-backend)
- Library Frontend (Angular) - [wlib-frontend](https://github.com/ctadel/wlib-frontend)

---

## Dockerhub Repositories

- Backend - [Backend](https://hub.docker.com/r/ctadel/backend-library)
- Frontend - [Frontend](https://hub.docker.com/r/ctadel/frontend-library)

---

## 👤 Author

Maintained by [ctadel](https://github.com/ctadel)

---

## ✉️ License

MIT License
