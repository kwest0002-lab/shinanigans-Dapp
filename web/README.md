# shinanigans-Dapp Web Application

This directory contains the full-stack web application for shinanigans-Dapp, divided into the backend service and the frontend client.

## Structure

```
web/
├── backend/    # NestJS REST & WebSocket API, PostgreSQL/TypeORM data access
└── frontend/   # Next.js (App Router), Tailwind CSS, React Query, Zustand
```

## Running Locally

### Backend (NestJS)

```sh
cd web/backend
npm install
npm run start:dev
```

The backend server runs on `http://localhost:3001` (or `3000` under Docker).

### Frontend (Next.js)

```sh
cd web/frontend
npm install
npm run dev
```

The frontend application runs on `http://localhost:3000`.

### Full Stack via Docker Compose

From the repository root:

```sh
docker compose up -d
```
