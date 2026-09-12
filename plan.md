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

- Review protraits, emotions for events

**Plan**:

1. (completed - verified in testing) `assets/schedules/Schedules.json` — add two entries to the marriage block of the dateable schedule patch: Send Robin to work on Saturdays & visit Caroline on Sundays
   - `marriage_Sat`: identical to `marriage_Sat` spec = copy of `marriage_Wed`
   - `marriage_Sun`: `1410 SeedShop 39 5 3/1700 bed` (home all morning, at SeedShop 39,5 from 1410, bed at 1700)
2. (completed) Robin should continue to visit Community Center after marriage, on Mondays, when the CC is completed: Marriage_Mon: 630 ScienceHouse 8 18 2/1700 CommunityCenter 9 19 3/1930 bed.
3. (completed - verified) Improve dialogue in Robin's 10-heart event
4. (completed - verified) Robin doesn't show up as 'wife' on relationships screen
5. (completed - verified) Prevent 'we got divorced' event from triggering for upgrading players who are already married
6. (completed - verified) Reworked the story & added two events to improve story pacing
7. (completed - verified) Added town-wide post-divorce gossip

**Status**: Implemented; verified.

---

## Technical Debt & Breakages Found

<!-- Log unexpected discoveries here during the project so you don't get sidetracked from the active task. -->

---

## Next Milestones (High-Level Backlog)

- Wedding day spritesheet needs a kissing sprite
- Add a note to Robin's space with her schedule
- Test if Robin goes to the GI Resort on Tuesdays (wins the lotto) after marriage.