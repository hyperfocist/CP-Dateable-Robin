# Current Plan & Context Bookmark

## Context Bookmark (Read This First After a Break)

- **Active Focus**: Milestone — Robin's Saturday & Sunday marriage schedules.
- **Next Immediate Step**: In-game retest — (1) as Robin's spouse: Sat = shop trip like Tuesday, Sun = home until 1410, at SeedShop 39,5, bed at 1700.
- **Interrupted State**: Both changes implemented (v1.1.0-beta.5); nothing committed yet.

---

## Recently Completed

- **Gate {{ModId}}\_0009 + RobinBecomesSingle TriggerAction by relationship status** (v1.1.0-beta.4, commit 4a87f57) — in-game test passed. Details in git history / Open Brain.
- **Robin's spawn location lags one day behind "Robin becomes single"** This was determined to be a mod conflict. The issue is resolved.

---

## Current Milestone: Robin needs a Saturday & Sunday marriage schedule

**Goal**: Robin needs a Saturday & Sunday marriage schedule.
Do this: marriage_Sat = Same as marriage_Wed. marriage_Sun = Robin arrive at SeedShop 39 5 3 at 1410, 1700 bed

**Plan**:

1. (completed) `assets/schedules/Schedules.json` — add two entries to the marriage block of the dateable schedule patch:
   - `marriage_Sat`: identical to `marriage_Sat` spec = copy of `marriage_Wed`
   - `marriage_Sun`: `1410 SeedShop 39 5 3/1700 bed` (home all morning, at SeedShop 39,5 from 1410, bed at 1700)
2. (to-do) Verify: JSON-validate `Schedules.json`; in-game test as Robin's spouse (Sat + Sun behavior).

**Status**: Implemented; in-game test pending.

---

## Technical Debt & Breakages Found

<!-- Log unexpected discoveries here during the project so you don't get sidetracked from the active task. -->

---

## Next Milestones (High-Level Backlog)

- Robin should continue to visit Community Center after marriage, on Mondays, when the CC is completed: Marriage_Mon: 630 ScienceHouse 8 18 2/1700 CommunityCenter 9 19 3/1930 bed.
- Robin doesn't show as "Married" on the in-game relationships screen, even though she is married to the player. Interestigly, the blue mermaid pendant icon does appear for her on this screen, as it should for a married NPC.
