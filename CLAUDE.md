# Timeline

A personal, single-page web app for putting events on a zoomable timeline. Each event has a name, optional description, a date and a significance from 1 to 20. Big events stay visible when zoomed out; minor ones appear as you zoom in. Several separate timelines ("World History", "My Life") can be created, renamed, switched and deleted. Used by Tim; no accounts, no backend.

- **Live:** https://timothyhadfield.github.io/timeline/
- **Repo:** https://github.com/TimothyHadfield/timeline (public)
- **Handoff state:** `progress.md` (read START HERE first)

## File map
- `index.html`: the whole app (inline CSS + plain JS, a `<canvas>` for the timeline). Sections in the script: data structures, init, timeline rendering (`renderTimeline`, `drawYear/Month/DayMarkers`, `getVisibleEvents`, `drawEvents`), interaction (wheel zoom, right-click drag, edge scroll, + / − / reset buttons), event CRUD, list (timeline) CRUD, utilities, persistence.
- `README.md`: the public showcase page for the repo (screenshots in `docs/screenshots/`).
- `docs/screenshots/desktop.png`, `phone.png`: README images only; the app doesn't load them.

## Data
- Everything is in the browser's `localStorage` key `timelineAppData` = `{ allLists: { <id>: { name, createdAt, events: [ { id, name, description, date: "YYYY-MM-DD", significance, createdAt } ] } }, currentListId }`. Ids are `Date.now()` strings.
- No server, so there is no shared or live user data in the repo. Never ask Tim for his browser data.

## Run locally
- `python -m http.server 8111` from the repo root (start it with the background option), then open http://localhost:8111/.
- Seed data for testing: `node ~/.claude/tools/phone-view.mjs http://localhost:8111/ --local "timelineAppData=<json>" ...` (a fresh browser profile each run, so it never touches Tim's data).

## Test
- No test suite and no build step. Verify with phone-view: `--do "click:.tab-btn:nth-child(3)"` opens the Timeline tab (`text=Timeline` matches the page heading instead). `--eval` can call the app's globals (`renderTimeline`, `getVisibleEvents`, `timelineState`, `loadList`, `formatDate`).
- Useful checks: event dots sit exactly on their day tick at day scale; the highest-significance events win overlaps; wheel zoom keeps the date under the mouse fixed.

## Deploy
- GitHub Pages, legacy build from `main` at `/`. Pushing to `main` publishes. Check with `python ~/.claude/hooks/live-check.py <repo path>`.

## Traps
- **Dates are local, never `new Date("YYYY-MM-DD")`** (that is UTC midnight, the previous evening in Utah). Use `parseLocalDate()` / `localDate()`; they use `setFullYear` so years below 100 (e.g. 79 AD) aren't turned into 19xx.
- Day ticks must step by calendar day (`setDate`), not by adding 24 h, or they drift across daylight-saving changes.
- Positions everywhere use `x = 100 (padding) + progress * (canvas.width - 200) * zoom + offsetX`. Wheel zoom, `getVisibleEvents` and `drawEvents` all assume that padding of 100.
- `getVisibleEvents` places events in significance order (so big ones win overlaps) but must return them in date order: `drawEvents` alternates above/below by that order.
- The canvas isn't scaled for devicePixelRatio, so it is soft on phones. Changing that is a visual change: Tim's call.
- Pan is right-click drag or mouse edge scroll only; there are no touch gestures. Tim's notes list Timeline as "laptop-first" (accepted).
- Deletes ask through the in-page `appConfirm()` (no browser `confirm()`); in phone-view click `#confirm-ok` / `#confirm-cancel` to answer it.

## Standing instructions
- No project-specific instructions from Tim yet. Tim owns the look, wording, layout and names; bug fixes must leave pixels unchanged unless he asks.
