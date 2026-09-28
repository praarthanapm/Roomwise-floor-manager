# Roomwise Smart-Search Floor Manager

This archive contains the Roomwise floor-manager web app, its source code, and the 10 uploaded timetable PDFs used to build the IST room schedule data.

## Run in the original Replit workspace

```bash
pnpm install
PORT=19377 BASE_PATH=/ pnpm --filter @workspace/floor-manager run dev
```

The app includes natural-language room search, floor and amenity filters, timetable-based availability, and add/edit/remove class controls.

Class changes are currently kept in browser session state and reset after a full refresh.
