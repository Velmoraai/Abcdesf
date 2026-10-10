# JEE Ascension V6.5.3 — Original-Deadline Backlog Penalties

Adaptive JEE command system.

## V5.7 changes
- Removed Weakness Bank, Question Log, and Revision pages.
- Added a dedicated Missed-Deadline Backlog.
- Added Daily Report: productive time, tasks completed, XP earned, target progress, activity history.
- Added Monthly Stats: six-month XP, productive-time, and task graphs plus a detailed table.
- Added editable daily and monthly XP targets.
- Activity logging powers the reports from task completion and productive timer XP.
- Existing unit/test deadlines, Reality Check, Priority Engine, Time Core, Test Hub, Progress Board, To-Do, and Course Library remain.

## GitHub Pages
Upload `index.html`, `style.css`, `app.js`, and `README.md` to the root of the repository. The tracker data stays in browser localStorage; do not upload exported JSON backups.


## Final verification
- Full V5.x feature set retained from the last complete codebase.
- Course Library URLs are real links; Add/Edit/Delete are implemented once each.
- Unit chapter checklist supports Add/Edit/Delete/Complete/Undo.
- Algebra checklist includes Sets, Relations & Functions, Complex Numbers, Quadratic Equations, Sequence & Series, P&C, Binomial, Matrices & Determinants, Statistics, Probability.
- Missed unit/test deadlines create backlog entries automatically.
- New missed deadlines deduct the configured XP penalty once and record the deduction.
- Existing localStorage key remains `jeeAscensionV5` so replacing the code does not intentionally create a new data store.


V6.1: Chapter-by-chapter unit checklist is now visible in both Deadline Radar and Progress Board. Checklist completion drives unit completion percentage and deadline urgency.


V6.2 adds editable subtasks to every To-Do task. Each task shows a live progress bar and completed/total count; subtasks can be added, checked, renamed, and deleted. Existing tasks are migrated with an empty subtasks list and existing tracker storage remains compatible.


V6.3 fixes the subtask buttons: task and subtask IDs are now quoted safely in inline event handlers, so Add, checkbox toggle, Edit, and Delete handlers receive valid arguments.


V6.4 fixes the Progress Board chapter-add control. The same unit checklist is rendered in both Progress Board and Deadline Radar; their add-chapter inputs now have separate IDs so each button reads the visible input. The button audit also checks that inline handlers resolve to defined functions, all rendered element IDs are unique, and renaming/deleting a unit deadline keeps its chapter data consistent.


## V6.5 — Daily backlog XP decay
- Replaces the new-deadline one-time XP hit with a recurring deduction for each unresolved backlog item.
- Default rate: 20 XP per active backlog item per calendar day; change it in Settings.
- The first daily deduction occurs the day after an item enters the backlog. If the tracker is not opened for several days, missed daily deductions are caught up on the next visit.
- Resolving an item stops future deductions. Reopening it restarts counting from the current date rather than charging for resolved days.
- XP cannot fall below zero; each item tracks penalty days and the actual XP deducted.
- Existing tracker storage key remains `jeeAscensionV5`. Existing historical one-time deductions are not refunded or repeated. Legacy active backlog items begin daily tracking from the first day V6.5 sees them; no historical daily deductions are backfilled.


## V6.5.2 — Backlog completion fix
- Completing a unit or test now automatically resolves its linked missed-deadline backlog item, stopping future daily XP deductions.
- If a unit/test is reopened after being auto-resolved, its linked backlog item becomes active again and daily counting restarts from the current date.
- Manually resolved backlog items remain resolved.
- Rechecked daily catch-up, same-day duplicate prevention, unit/test completion, reopening behavior, and manual resolution.


V6.5.2 fix: deleting a unit deadline or test now resolves its linked automatic backlog item, preventing further daily XP deductions from an item whose source was deleted. Existing XP history and the localStorage key remain unchanged.


## V6.5.3 — Original-deadline-based backlog penalties
- Newly detected automatic backlog items use their original unit/test deadline as the penalty date anchor.
- Daily XP deductions begin the calendar day after the original deadline, not the day the tracker first notices the missed deadline.
- If the tracker is closed, the next visit catches up daily deductions from the original deadline through the current date.
- Existing backlog items created by earlier versions are not retroactively recalculated; their recorded penalty dates and history are preserved.
- Existing localStorage key remains `jeeAscensionV5`.
