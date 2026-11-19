# DevTrackr

A small project tracker with a Spring Boot API and a Next.js frontend.

## What it does

- Register and log in (JWT).
- Create, edit and delete projects with a name, description, due date and status: `PENDING`, `ACTIVE` or `COMPLETED`.
- Change a project's status with a single call.
- List projects with pagination and sorting, filter by status, and search from the UI.

## How it works

The frontend talks to the backend at `/api` (default `http://localhost:8080/api`) with Axios and TanStack Query. The JWT is kept in `localStorage` and sent as a Bearer token. Spring Security is stateless: everything except `/api/auth/**` needs a token. Tables are created by Hibernate (`ddl-auto=update`), so there are no migrations.

Endpoints: `POST /api/auth/register`, `POST /api/auth/login`, and `GET, POST /api/projects`, `GET, PUT, DELETE /api/projects/{id}`, `PATCH /api/projects/{id}/status`. See `backend/API_DOCUMENTATION.md`.

## Stack

- **Backend:** Java 17, Spring Boot, Spring Security, Spring Data JPA, jjwt, PostgreSQL
- **Frontend:** Next.js 16, React 19, Tailwind CSS 4, TanStack Query and Table, react-hook-form, zod, GSAP and three.js for the landing visuals

## Run it locally

You need Java 17, Node.js with pnpm, and a PostgreSQL database named `devtrackr`.

```bash
# backend, on :8080
cd backend
./mvnw spring-boot:run

# frontend, on :3000
cd frontend
pnpm install
pnpm dev
```

The database URL, username, password and JWT secret are read from `backend/src/main/resources/application.properties` (`spring.datasource.*`, `jwt.secret`, `jwt.expiration`). Set your own before running. The frontend reads `NEXT_PUBLIC_API_URL` if the API isn't on `localhost:8080`; its login and register route handlers point at `http://localhost:8080/api` directly.

## Notes

A personal project from November 2025. It doesn't track tech stacks or progress, only status and due date. Projects are shared across all users, not scoped per account. A database password and a JWT secret are committed in `application.properties`, so treat them as burned and move them to environment variables before deploying anything. There are no tests beyond the Spring context test.
