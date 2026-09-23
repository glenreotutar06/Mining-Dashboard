# Global Geologica — Mining Business Unit Dashboard

A self-contained, dependency-free dashboard (no build step, no external libraries —
just `index.html` + `tasks_rev1.csv`). Deploy the two files together, in the same
folder, to any static host.

## What's in this folder

- `index.html` — the dashboard
- `tasks_rev1.csv` — the task data it displays

The dashboard automatically tries to `fetch("tasks_rev1.csv")` from wherever it's
hosted. If that file is present next to it, the dashboard is **live-linked**: it loads
the current data on open and re-checks every 60 seconds, so updating the CSV on the
server is all it takes to push new data to everyone viewing the page. If the fetch
fails (no server, or the CSV is missing), it falls back to a snapshot of the data
that's embedded directly in `index.html`.

## Updating the data

Replace `tasks_rev1.csv` with a newer export (same column headers) and re-upload just
that one file — no need to touch or re-deploy `index.html`. Anyone with the page open
picks up the change within 60 seconds; a fresh page load picks it up immediately.

## Deploy it — three options

### Option A: Netlify (fastest — drag and drop, no account setup beyond signing in)
1. Go to [app.netlify.com/drop](https://app.netlify.com/drop)
2. Drag this whole folder (both files) onto the page
3. Netlify gives you a live URL immediately (e.g. `random-name-123.netlify.app`)
4. To update later: drag the folder again, or connect it to a GitHub repo for git-based deploys

### Option B: GitHub Pages (free, tied to a GitHub repo)
1. Create a new GitHub repository (or use an existing one)
2. Add `index.html` and `tasks_rev1.csv` to the repo root (or a `/docs` folder)
3. Go to the repo's Settings → Pages, set the source to the branch/folder you used
4. GitHub gives you a URL like `https://yourusername.github.io/repo-name/`
5. To update: commit and push a new `tasks_rev1.csv` (or `index.html`)

### Option C: Cloudflare Pages / Vercel
Both work the same way as Netlify — connect a GitHub repo or drag-and-drop the folder;
no build command is needed since there's nothing to build.

## Sharing internally without public hosting

If the data is sensitive and you'd rather not use a public static host, host these two
files on an internal web server or intranet site instead — anywhere that can serve
plain static files over HTTP works, since there's no server-side logic at all.

## A note on the embedded snapshot

Every time you replace `tasks_rev1.csv` going forward, the *live* data updates
automatically (per above) — but the *embedded snapshot* baked into `index.html`
stays frozen at whatever it was when this file was generated. That's fine for normal
use (it's only a fallback), but if you want the fallback itself to reflect newer data
too, ask Claude to refresh the embedded snapshot from a new CSV.
