# AGENTS.md

## Project overview

This repository is the Angular frontend for a condominium management system. The app is organized by domain features and uses lazy-loaded Angular modules for routing. The backend is separate from this repo and is expected to run externally (ASP.NET Core + RabbitMQ + SQL Server) on the Docker network `infra_net`.

Primary references:
- [README.md](README.md)
- [STYLE_GUIDE.md](STYLE_GUIDE.md)
- [docker-compose.yml](docker-compose.yml)

## Working conventions

- Keep domain features under `src/app/pages` using the existing pattern: `*-module.ts`, `*-routing-module.ts`, `services`, form components, and list components.
- Reusable app infrastructure belongs in `src/app/core` and `src/app/shared` instead of feature folders.
- Prefer lazy loading for pages via `loadChildren` in [src/app/app-routing-module.ts](src/app/app-routing-module.ts).
- Use the existing Portuguese naming and domain language (for example: `empresas`, `imoveis`, `moradores`, `usuarios`).
- Keep configuration in `src/environments` rather than hardcoding service URLs or credentials.
- Follow the design system described in [STYLE_GUIDE.md](STYLE_GUIDE.md): prefer shared classes such as `.btn`, `.form-control`, `.itens-table`, and spacing tokens instead of ad hoc inline styling.
- This app is localized for Brazilian Portuguese; keep `pt-BR` conventions intact when working with date/number formatting or locale-sensitive UI.

## Standard validation commands

Run these from the repository root:

- Install dependencies: `npm install`
- Start the app locally: `npm run start`
- Build the app: `npm run build`
- Watch mode: `npm run watch`
- Run unit tests: `npm run test`
- Start via Docker: `docker-compose up --build -d`

## Architecture notes

- The app bootstraps in [src/app/app-module.ts](src/app/app-module.ts) and uses the root routing config in [src/app/app-routing-module.ts](src/app/app-routing-module.ts).
- `AuthGuard` and layout components live under `src/app/core`, while domain pages are isolated under `src/app/pages`.
- Shared UI primitives and reusable components live under `src/app/shared`.
- The frontend is expected to integrate with an external backend API and does not contain the application server implementation itself.

## Guidance for agent work

- Prioritize minimal, localized edits that match the repo’s feature-module structure.
- When adding UI, follow the existing patterns already used in similar page modules and shared components.
- When changing a page or service contract, verify the related Angular module and route still line up with the surrounding architecture.
- Do not invent a new project structure or rework the app into a different pattern unless the task explicitly requires it.
- Prefer existing naming, folder boundaries, and styles over introducing brand-new conventions.
