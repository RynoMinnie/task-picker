# Changelog

All notable changes to this project are documented here. Version numbers follow
[Semantic Versioning](https://semver.org/) (MAJOR.MINOR.PATCH):
- **MAJOR** — breaking changes (e.g. saved task lists no longer load correctly)
- **MINOR** — new features, backward compatible
- **PATCH** — bug fixes, small tweaks

When you bump the version, update it in all three places:
1. `APP_VERSION` constant in `index.html`
2. `"version"` field in `manifest.json`
3. A new entry at the top of this file

## v1.0.0 — 2026-09-07

Initial packaged release. Converted the app from a Claude-artifact prototype into a
standalone, installable web app.

**Added**
- Weighted random task picker with an animated spinning wheel (SVG, per-task colors)
- Adjustable per-task probability weight (1–10 slider)
- Adjustable per-task countdown timer (in minutes)
- Start / Pause / Reset controls for the active task's timer
- Repeating audio alarm when a timer reaches zero (stops on Complete, Clear, Reset, or next spin)
- Complete / Clear actions for the currently selected task
- Completed-tasks history log, with a "Clear history" reset
- Automatic weight decay (−1, floor of 1) each time a task is completed
- "Reset weights" button that restores each task to the weight you last manually set
  (not a fixed default — tracked separately as each task's `baseWeight`)
- Drag-and-drop task reordering (grab the ⋮⋮ handle)
- Export task list to a `.json` file / Import a `.json` file back in, with a
  Replace-or-Merge choice when you already have tasks loaded
- Browser tab title shows the active task name and live countdown
- Countdown is timestamp-based so it stays accurate even if the browser throttles
  the tab in the background, and re-syncs the instant the tab regains focus
- Screen Wake Lock requested while a timer is running, to stop the screen sleeping
- Packaged as an installable Progressive Web App: `manifest.json`, `service-worker.js`,
  and a generated icon set (`icons/`), so it can be installed from the browser or
  submitted to the Microsoft Store / Google Play via PWABuilder
- In-app version number shown at the bottom of the task list

**Changed**
- Persistent storage switched from Claude's `window.storage` API (only available inside
  Claude chats) to the browser's own `localStorage`, via a small compatibility shim, so
  the app works as a normal standalone website. Task lists no longer sync automatically
  between devices — use Export/Import to move a list between browsers or devices.

**Fixed**
- Corrected a sign error in the wheel's rotation math that could land the pointer on a
  different segment than the one actually picked.
