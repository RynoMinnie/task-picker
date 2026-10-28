# What's Next? — Task Picker

A weighted random task picker: add your to-do items, decide how likely each one is to
come up, spin a wheel to pick what to do next, then run a built-in timer for it.

**Current version:** v1.0.0 — see [CHANGELOG.md](./CHANGELOG.md) for release history.

## Features

- Spinning wheel that picks a task at random, weighted by a per-task probability slider
- Per-task countdown timer (Start / Pause / Reset) with a repeating audio alarm at zero
- Complete or Clear the current pick; completed tasks are logged with a timestamp
- Task weights automatically decay by 1 each time you complete that task, so recently
  finished items come up less often — with a one-click "Reset weights" to put them back
  to what you last set them to
- Drag-and-drop reordering of your task list
- Export your task list to a file and import it back in — handy for switching between
  different task groups or moving your list to another device/browser
- Installable as a standalone app (desktop or mobile) — see [Installing it](#installing-it)
  below
- Works offline once installed

## Using it

1. Open the app (see [Hosting it](#hosting-it) below for how to get it a URL).
2. Type a task into the box and click **Add** (or press Enter).
3. Drag the weight slider for each task — higher means it's more likely to be picked.
   Set a timer length (in minutes) for each task too.
4. Click **Spin**. The wheel lands on a task, weighted by those sliders.
5. Click **Start** to begin the countdown for that task. **Complete** logs it as done
   and slightly reduces its weight; **Clear** just dismisses the pick without logging it.
6. Use **Export** / **Import** at any time to save or load a task list as a `.json` file.

Your task list is saved automatically in the browser you're using (not synced across
devices — use Export/Import to move it).

## Hosting it

This is a fully static site — no server or build step required. Any static host works:
GitHub Pages, Netlify, Vercel, etc. To use GitHub Pages:

1. Push this folder to a GitHub repository (see the repo's own instructions if you're
   setting this up for the first time).
2. In the repository, go to **Settings → Pages**, set the source to your main branch
   and the `/` (root) folder, then save.
3. GitHub gives you a URL like `https://yourusername.github.io/your-repo-name/`.

## Installing it

Once it's hosted somewhere with a real URL (not just opened as a local file), most
browsers offer to install it as an app:

- **Desktop Chrome / Edge:** look for an install icon in the address bar, or use the
  browser menu → "Install app" / "Apps → Install this site as an app".
- **Android Chrome:** you'll get an "Install" or "Add to Home screen" prompt.
- **iPhone/iPad Safari:** use the Share button → "Add to Home Screen".

Installed, it opens in its own window with its own icon, and works offline.

### Publishing to the Microsoft Store / Google Play

Once the app is hosted and installable, run its URL through
[PWABuilder](https://www.pwabuilder.com/) to generate packages for:
- **Microsoft Store** — free for individual developer accounts
- **Google Play** — one-time $25 developer account fee

PWABuilder reads `manifest.json` and `service-worker.js` automatically — no extra setup
needed on top of what's already in this project.

## Project structure

```
index.html          The entire app: markup, styles, and logic in one file
manifest.json        PWA manifest (name, icons, colors, version) — used for install
                      prompts and by PWABuilder for store packaging
service-worker.js    Enables offline use once installed
icons/                App icons (192px, 512px, and a maskable 512px variant)
CHANGELOG.md          Version history — update this whenever you bump the version
README.md             This file — update it whenever features or setup steps change
worklog.md            Development handover log (kept locally, not pushed to GitHub —
                      see .gitignore)
.gitignore
```

## Making changes / versioning

- The version number lives in three places that should always match: the
  `APP_VERSION` constant near the top of the `<script>` in `index.html`, the
  `"version"` field in `manifest.json`, and the latest entry in `CHANGELOG.md`.
- Bump the **patch** number for small fixes, **minor** for new features, **major** for
  anything that changes how saved data is stored (see `CHANGELOG.md` for the full
  convention).
- After any change: update `CHANGELOG.md`, update this README if usage or setup
  changed, and log the change in `worklog.md`.

## Notes on data storage

Task lists, completed history, and weights are stored in the browser's `localStorage`
— private to that browser on that device. There's no server and no account. If you
clear your browser's site data, or switch browsers/devices, your list won't carry over
automatically — use **Export** beforehand and **Import** on the other side.
