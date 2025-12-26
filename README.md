# TenantProject UI ⚙️

**TenantProject UI** is the front-end application (Vite + Vue 3 + TypeScript) for managing tenants, registration, and the administration dashboard.

---

## 📌 Overview

- Core stack: **Vue 3**, **TypeScript**, **Vite**
- HTTP client: **axios** (configured in `src/services/api.ts` using `VITE_API_URL`)
- State & logic: composable hooks under `src/composables` (e.g. `auth`, `tenants`)
- Dockerized build: uses **bun** for the build stage and **nginx** for serving (see `Dockerfile` and `nginx.conf`).

---

## 📖 Key Features

- Tenant management (list, create)
- SPA routing fallback handled by `nginx.conf`

---

## 🚀 Quick Start

### Prerequisites

- Node.js (recommended) or Bun (used in Docker image build)
- npm / pnpm / yarn
- Docker & docker-compose (optional, for containerized deployment)

### Run locally

1. Install dependencies:

```bash
npm install
# or using bun: bun install
```

2. Prepare environment file:

```bash
cp .env.local.example .env.local
# then set VITE_API_URL (e.g. http://localhost:5001)
```

3. Start dev server:

```bash
npm run dev
```

4. Build production bundle:

```bash
npm run build
```

5. Preview production build (locally):

```bash
npm run preview
```

> Note: The `Dockerfile` runs `bun run build` when building the image — intended for pipeline/container builds.

---

## 🐳 Using Docker

- Build and run with docker-compose:

```bash
docker-compose up --build
```

- The service in `docker-compose.yaml` maps host port `5003` to container port `80` (access via `http://localhost:5003`).

---

## 🔧 Configuration & Environment

- Important variable: `VITE_API_URL` → backend API base URL
- Example development file: `.env.development` contains:

```
VITE_API_URL=http://localhost:5001
```

- CI/CD: the workflow in `.github/workflows/ci.yml` writes `VITE_API_URL` into `.env.local` using repo secrets.

---

## 🗂️ Important Files / Structure

- `src/services/api.ts` — axios configuration (baseURL = `import.meta.env.VITE_API_URL`)
- `src/composables` — reusable logic (auth, tenants, etc.)
- `src/views` — application pages (auth, tenants, admin, home, 404)
- `Dockerfile` — multi-stage build (bun → nginx)
- `nginx.conf` — static server configuration + SPA fallback

---

## 🧪 Debug & Troubleshooting

- If the API is unreachable, check `VITE_API_URL` in `.env.local` or `.env.development`.
- If Docker build fails, verify `bun` works correctly in the `oven/bun:1` image.

---

## 🤝 Contributing

Please open an issue or submit a pull request. Include a description of the change and reproduction steps when applicable.

---

## 📄 License

Default license: **MIT** — adjust as needed.

---

If you'd like, I can also add CI/CD badges, testing instructions, or example curl requests for the API endpoints. 💡
