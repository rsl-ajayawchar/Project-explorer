# Project Explorer — Next.js App Router Assignment

A responsive project management portal demonstrating modern Next.js App Router patterns with TypeScript, React Server Components, Client Components, nested layouts, dynamic and catch-all routes, URL search parameters, loading/error states, and Suspense streaming.

## Requirements covered

- **Shared layout:** root `app/layout.tsx` provides global navigation, metadata, styling, and footer.
- **Pages:** Home, About, Dashboard, Projects, Settings, plus Analytics, Reports, and Team dashboard pages.
- **Dashboard-only layout:** `app/dashboard/layout.tsx` adds a dashboard sidebar only to dashboard routes.
- **Project module:** JSON-backed project list and dynamic detail pages at `/projects/[id]` with nested Overview, Team, Tasks, Activity, and Docs tabs.
- **Catch-all route:** `/projects/[id]/docs/[...slug]` displays the full requested resource path, e.g. `/projects/1/docs/setup/database`.
- **URL filters:** `/projects?search=nextjs&status=active` is parsed on the server; the hydrated filter controls update query parameters without losing the other filter.
- **Loading:** `app/projects/loading.tsx` provides skeleton UI during project route loading.
- **Error handling:** `app/projects/error.tsx` provides a friendly retry UI; invalid project IDs use `app/projects/[id]/not-found.tsx`.
- **Streaming:** dashboard uses an async Server Component with a simulated delay wrapped in `Suspense`, so the rest of the dashboard can render first.
- **Client-side interactivity:** Settings theme toggle persists the selected theme in localStorage; project search and status controls are Client Components.
- **Bonus:** responsive styling, local JSON dataset, custom not-found page, reusable skeletons, and extra dashboard routes.

## Run locally

Use Node.js 20.9+ (recommended for Next.js 15) and npm.

```bash
npm install
npm run dev
```

Open http://localhost:3000.

To check a production build:

```bash
npm run build
npm start
```

## Useful routes

- `/`
- `/about`
- `/dashboard`
- `/dashboard/analytics`
- `/dashboard/reports`
- `/dashboard/team`
- `/projects`
- `/projects?search=dashboard&status=active`
- `/projects/1`
- `/projects/1/team`
- `/projects/1/tasks`
- `/projects/1/activity`
- `/projects/1/docs/setup/database`
- `/settings`
- `/projects/999` (custom not-found UI)

## Architecture notes

Most pages and data reads are Server Components by default. Client Components are limited to interactive browser behavior in `components/project-filters.tsx` and `components/theme-toggle.tsx`. The `ProjectFilters` component uses `useSearchParams`, so it is wrapped in `Suspense` in the Projects page to support static rendering. Project details use a shared nested layout to keep the project heading and tabs consistent while moving between sections.

The project dataset is a demo fixture in `lib/projects.json`; replace it with a real API/database when integrating a backend. The dashboard activity delay is intentionally simulated to demonstrate streaming.

## GitHub / PR / demo deliverables

This source bundle does not create a GitHub repository, push a branch, open a PR, or upload a video to Google Drive. After reviewing and running the project, create a branch (suggested: `feature/project-explorer-app-router`), push it to your repository, open a PR, and record the required walkthrough. Add the PR and Drive links to your completion status email.
