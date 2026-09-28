# Smart-Search Floor Manager

Roomwise helps students find empty campus rooms from timetable availability using natural-language search and traditional filters.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/floor-manager/src/App.tsx` — the Phase 1 room dataset, timetable availability logic, natural-language parser, and single-page UI.
- `artifacts/floor-manager/src/index.css` — the Roomwise theme tokens, typography, motion, and shared base styles.
- `artifacts/floor-manager/.replit-artifact/artifact.toml` — web artifact routing and production build configuration.

## Architecture decisions

- The timetable model stays local to the web artifact so availability updates immediately as the student changes the search window or edits a class.
- Natural-language search is parsed into a typed search intent, then combined with manual filters before room availability is calculated.
- Availability is derived from timetable block overlap for the selected day, start time, and duration; room status is never stored as a hardcoded flag.
- Uploaded timetable PDFs are represented by their IST venue, section, course, and faculty details; class edits are local to the current session in Phase 1.

## Product

- Students can search for rooms using everyday language, including floor, duration, capacity, AC, and projector requirements.
- Results are grouped floor-by-floor and show open or in-use state for the selected time window.
- Selecting a room reveals capacity, amenities, and the relevant day’s timetable blocks.
- The current dataset maps the 10 uploaded timetable sources to IST 225, 227, 211, 411, 416, 518, 519, 602, 617, and 710.
- Students can open "Change classes" from a room, edit a class, add a class, or remove a class; each change recalculates room availability immediately.

## User preferences

None recorded.

## Gotchas

- Keep timetable times in minutes from midnight so overlap checks remain simple and duration-aware.
- If more timetable sources are added, preserve the room fields and block shape used by the parser, grid, and class editor.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
