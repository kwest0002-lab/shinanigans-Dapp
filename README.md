# shinanigans-Dapp

shinanigans-Dapp is an open-source inventory and asset management system built to help organizations register, track, monitor, and manage physical and digital assets across teams, locations, and regions.

The platform is designed for businesses that need visibility and accountability over their assets without relying on fragmented spreadsheets or rigid legacy software. shinanigans-Dapp provides a centralized system for asset lifecycle management while remaining flexible enough to adapt to different organizational structures.

---

## Motivation

As organizations grow, asset tracking often becomes inconsistent. Equipment is moved between departments, licenses are shared across teams, and assets are duplicated or lost due to poor visibility.

Common challenges include:

- No single source of truth for asset ownership
- Limited tracking across branches or countries
- Manual updates and inconsistent records
- Difficulty auditing asset usage and history

shinanigans-Dapp addresses these issues by offering a structured, auditable system that tracks assets from registration through retirement.

---

## What shinanigans-Dapp Provides

shinanigans-Dapp enables organizations to:

- Register physical and digital assets
- Assign assets to departments, users, or locations
- Track asset status, condition, and movement
- Maintain asset history and lifecycle events
- Generate reports for audits and decision-making

The system is designed to scale from small teams to multi-branch organizations.

---

## Key Capabilities

- Asset registration and categorization
- Department and location-based ownership
- Asset lifecycle tracking (active, assigned, retired)
- History and change logs
- Search and filtering across asset records
- Role-based access control

---

## System Architecture

The codebase is divided into two primary parts:

1. **`contracts/` (Smart Contracts)**: On-chain asset registry, multisig governance, maintenance history, staking, and escrow built on Stellar/Soroban in Rust.
2. **`web/` (Web Application)**: Full-stack application comprising:
   - `web/backend/`: NestJS REST & WebSocket API, PostgreSQL/TypeORM database, and Redis caching.
   - `web/frontend/`: Next.js web interface with Tailwind CSS, React Query, and Zustand.

---

## Technology Stack

### Contracts (Rust)
- Stellar / Soroban SDK (v23)
- Rust (pinned toolchain: 1.96.0)

### Web Application (TypeScript)
- **Frontend**: Next.js 15, TypeScript, Tailwind CSS, React Query, Zustand, React Hook Form, Zod
- **Backend**: NestJS, PostgreSQL 16, TypeORM, Redis 7, Socket.io, BullMQ

---

## Installation

### Prerequisites

- Node.js (v18 or newer)
- PostgreSQL (v14 or newer)
- npm or yarn
- Git

---

### Clone the Repository

```bash
git clone https://github.com/your-org/shinanigans-dapp.git
cd shinanigans-Dapp
```

---

### Smart Contracts Setup (Rust)

```bash
cd contracts
cargo build --all
cargo test --all
```

---

### Backend Setup (NestJS)

```bash
cd web/backend
npm install
```

Create a `.env` file:

```env
DATABASE_HOST=localhost
DATABASE_PORT=5432
DATABASE_USER=postgres
DATABASE_PASSWORD=postgres
DATABASE_NAME=shinanigans_dapp
```

Run database migrations:

```bash
npm run migration:run
```

Start the backend server:

```bash
npm run start:dev
```

The backend will be available at `http://localhost:3001`.

---

### Frontend Setup (Next.js)

```bash
cd web/frontend
npm install
npm run dev
```

The frontend will be available at `http://localhost:3000`.

---

## Usage

1. Create an account or sign in
2. Set up departments, locations, and asset categories
3. Register assets with relevant details
4. Assign assets to users or departments
5. Track asset status and history over time

Assets can be updated, transferred, or retired as organizational needs change.

---

## Development

### Running Tests

```bash
npm run test
```

### Linting

```bash
npm run lint
```

---

## Contributing

Contributions are welcome from developers and product engineers.

To contribute:

1. Fork the repository
2. Create a feature branch
3. Submit a pull request with a clear description of your changes

- Include a **deployment section (Docker / CI)**
- Write a **more enterprise-focused version** for internal tools

## Quickstart with Docker

The fastest way to get the backend running locally with a matching Postgres 16 and Redis 7 (same versions as CI) is via Docker Compose.

### Prerequisites

- Docker and Docker Compose installed

### Run it

```bash
git clone <repo-url>
cd shinanigans-Dapp
docker compose up
```

This brings up three containers:

| Service    | Description                             | Port |
| ---------- | --------------------------------------- | ---- |
| `postgres` | Postgres 16, data persisted in a volume | 5432 |
| `redis`    | Redis 7, data persisted in a volume     | 6379 |
| `backend`  | NestJS API in watch mode (`start:dev`)  | 3000 |

No manual Postgres/Redis install or configuration is required — the backend
container is pre-wired with the same env var names used in
`.github/workflows/backend-ci.yml` (`DB_HOST`, `DB_PORT`, `DB_USERNAME`,
`DB_PASSWORD`, `DB_NAME`, `REDIS_HOST`, `REDIS_PORT`, `JWT_SECRET`).

The API will be available at `http://localhost:3000` once all three
containers report healthy.

### Overriding defaults

Create a `.env` file at the repo root to override any default credentials
before running `docker compose up`:

```bash
DB_USERNAME=postgres
DB_PASSWORD=postgrespassword
DB_NAME=shinanigans_dapp_dev
JWT_SECRET=dev-secret-key
```

### Stopping / resetting

```bash
docker compose down          # stop containers, keep data
docker compose down -v       # stop containers and wipe Postgres/Redis volumes
```

### Building a production image

The backend `Dockerfile` is multi-stage. `docker compose up` builds the
`development` target (hot reload). To build the production image used for
deployment:

```bash
docker build --target production -t shinanigans-dapp-backend ./web/backend
```
