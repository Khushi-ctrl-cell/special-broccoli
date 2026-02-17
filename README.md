# Green Quest - Sustainability Gamification Platform

Full-stack sustainability gamification platform with React (Vite + Tailwind) frontend, Node.js/Express backend, PostgreSQL database, and Prisma ORM.

## Architecture

- **Client** (`/client`): React + Vite + Tailwind + shadcn/ui
- **Server** (`/server`): Node.js + Express + Prisma + JWT auth
- **Database**: PostgreSQL

## Prerequisites

- Node.js 18+
- PostgreSQL
- npm or pnpm

## Quick Start

### 1. Install Dependencies

```bash
npm install
cd client && npm install
cd ../server && npm install
```

### 2. Environment Variables

**Server** - Create `server/.env`:

```env
DATABASE_URL="postgresql://user:password@localhost:5432/green_quest?schema=public"
JWT_SECRET="your-super-secret-jwt-key-change-in-production"
PORT=3001
NODE_ENV=development
```

**Client** - Create `client/.env` (optional, for custom API URL):

```env
VITE_API_URL=http://localhost:3001/api
```

If not set, the client uses `/api` which is proxied to the server in dev.

### 3. Database Setup

```bash
cd server
npx prisma migrate dev --name init
npx prisma db seed
```

### 4. Run the Application

**Development** (runs both client and server):

```bash
npm run dev
```

- Frontend: http://localhost:8080
- Backend API: http://localhost:3001

**Or run separately:**

```bash
# Terminal 1 - Backend
cd server && npm run dev

# Terminal 2 - Frontend
cd client && npm run dev
```

### 5. Production Build

```bash
npm run build
npm start
```

Serve the `client/dist` folder with a static file server (e.g. nginx) and point API requests to the backend.

## Default Admin Account

After seeding:
- Email: `admin@greenquest.com`
- Password: `admin123`

## API Endpoints

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| POST | /api/auth/signup | No | Register |
| POST | /api/auth/login | No | Login |
| GET | /api/users/me | Yes | Current user |
| GET | /api/users/leaderboard | No | Leaderboard |
| GET | /api/quests | No | List quests |
| GET | /api/quests/me | Yes | My completed quests |
| POST | /api/quests/complete | Yes | Complete a quest |
| POST | /api/quests | Admin | Create quest |
| PUT | /api/quests/:id | Admin | Update quest |
| DELETE | /api/quests/:id | Admin | Delete quest |

## Scripts

| Script | Description |
|--------|-------------|
| `npm run dev` | Run client + server in dev mode |
| `npm run build` | Build client + server |
| `npm start` | Run production server |
| `npm run db:migrate` | Run Prisma migrations |
| `npm run db:seed` | Seed database |
