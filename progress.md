# Timeline: progress

## START HERE
Last updated 2026-10-16. Read order: `CLAUDE.md` (what the app is, file map, traps), then this file. There is no `chat.md` yet.

## Goal right now
Maintenance only. The app is published and working; no feature work is planned.

## Status
| Area | State |
|---|---|
| App (`index.html`) | Live at https://timothyhadfield.github.io/timeline/ |
| Tests | None (single HTML file); verified with phone-view `--eval` checks |
| Repo | Public, published 2026-09-27 with README and screenshots |
| 2026-10-16 sweep | 7 logic bugs fixed (see Decisions); CLAUDE.md and this file added |

## Authorized next steps
None.

## Standing instructions
- None specific to this project yet (global rules apply).

## Traps
- See `CLAUDE.md` Traps (local dates, DST-safe day stepping, padding of 100 in all x math).
- No accounts, so no `claude-test` account is needed.

## Decisions
- 2026-10-16 sweep: biggest events now win overlaps (Apollo 11, significance 20, was hidden behind smaller events); event dots line up with their day ticks (they were drawn at UTC midnight, 6-7 h early); years below 100 no longer show as 19xx; day ticks no longer repeat or skip around daylight-saving changes or month ends; wheel zoom no longer drifts off the mouse; hovering the zoom buttons no longer pans the view, and leaving the window from an edge stops edge scrolling; on phones the help box no longer sits under the zoom buttons.

## NOT verified
- Real iPhone (only WebKit at 393 px via phone-view). The timeline tab uses `height: 100vh`, which on iOS Safari can be taller than the visible area.
- Year labels at extreme zoom-out over very long ranges (more than ~1000 years) may crowd; not tested.

## Rejected / parked
- Nothing yet.
