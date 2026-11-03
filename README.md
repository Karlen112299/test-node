# Task App

A full-stack task manager built as an npm-workspaces monorepo.

- **Client:** React, TypeScript, Redux Toolkit, React Router (Vite)
- **Server:** Node.js, Express, TypeScript, Zod

## Prerequisites

- **Node.js 22.12+** (or 20.19+). Check with `node -v`
- **npm 10+**. Check with `npm -v`

## Getting started

```bash
# 1. Clone the repository
git clone <repo-url>
cd <repo-folder>

# 2. Install all dependencies (client + server) from the root
npm install

# 3. Create the server environment file
cp server/.env.example server/.env

# 4. Start both apps in development mode
npm run dev
```

Once running:

| Service | URL                              |
| ------- | -------------------------------- |
| Client  | http://localhost:5173            |
| Server  | http://localhost:4000            |
| Health  | http://localhost:4000/api/health |

The Vite dev server proxies any `/api/*` request to the Express server, so no extra CORS or URL configuration is needed locally.

## Environment variables

Defined in `server/.env` (see `server/.env.example`):

| Variable | Default | Description      |
| -------- | ------- | ---------------- |
| `PORT`   | `4000`  | Port for the API |

## Scripts

Run from the repository root:

| Command         | Description                                 |
| --------------- | ------------------------------------------- |
| `npm run dev`   | Start server and client together            |
| `npm run build` | Build both server and client for production |

Run a single app:

```bash
npm run dev -w server
npm run dev -w client
```

## Project structure

```
.
├── client/                 # React app
│   └── src/
│       ├── app/            # Redux store, typed hooks
│       ├── features/       # Redux slices and feature UI
│       ├── components/     # Shared UI components
│       ├── pages/          # Route-level pages
│       └── api/            # API client
├── server/                 # Express API
│   └── src/
│       ├── config/         # Environment loading
│       ├── routes/         # URL to controller mapping
│       ├── controllers/    # HTTP layer (req/res)
│       ├── services/       # Business logic
│       ├── middleware/     # Error handling, validation, auth
│       ├── app.ts          # Express app setup
│       └── server.ts       # Entry point
└── package.json            # Workspace configuration
```

The server follows a layered architecture: **routes → controllers → services**.

## API

| Method | Endpoint      | Description  |
| ------ | ------------- | ------------ |
| GET    | `/api/health` | Health check |

More endpoints are documented here as they are added.

## Troubleshooting

**`Cannot find native binding` (rolldown) when starting the client**
This is a known npm optional-dependencies bug. From the root:

```bash
rm -rf node_modules package-lock.json client/node_modules server/node_modules
npm install
```

**`EBADENGINE` warnings or unexpected build errors**
Your Node version is too old. Upgrade to 22.12+ (for example, `nvm install 22 && nvm use 22`).

**Port already in use**
Change `PORT` in `server/.env`, or stop the process using port 4000 or 5173.
