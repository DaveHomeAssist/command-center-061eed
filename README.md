# Command Center

A private, single-page ops dashboard that gives Dave a one-screen view of all his active projects — status, git sync state, domain health, daily automation runs, and open triage items. The page is `noindex, nofollow` and carries no login; privacy comes only from the URL being unlisted.

This repo is a **publish mirror**, not a source workspace. The dashboard is authored and rendered elsewhere (in a local `ops-hub` workspace, from `quick-start/render.mjs` + a JSON source registry) and pushed here verbatim by `ops-hub/quick-start/publish-061eed.sh`, which the ops-hub automation calls on every reconcile pass. There is no build step, editable source, or package manifest in this repo — `index.html` is the deployed artifact itself.

## What's here

| Path | What it is |
|---|---|
| `index.html` | The dashboard — a single static HTML file (styles, script, and data all inline). Rendered and overwritten wholesale on every republish; never hand-edited in place. |
| `skill-library/` | A secondary static page (`index.html` + `skills-data.js`) that browses Dave's Claude Code skill library. `skills-data.js` is auto-generated ("do not edit by hand") by a `generate-data.py` script that lives in the ops-hub source workspace, not here. |
| `.github/workflows/republish-from-ops-hub.yml` | An older, manually-triggered (`workflow_dispatch`) publish path that assembled `index.html` from staged `_cc_chunks/*.html`. It appears superseded by `publish-061eed.sh`'s direct-push flow (which is how nearly all recent commits actually land) but is left in place. |
| `.nojekyll` | Disables Jekyll processing so GitHub Pages serves `index.html` as-is. |
| `LICENSE` | All-rights-reserved. |

The dashboard itself surfaces panels for: Overview, Garden OS, ReadOut, Phillies Wire, PromptLab, PlotForge, Hat-in-Ring, Home Assistant, System by Dave, Festival Atlas, CurlPlan, Davai, Metagrid, Attention, Today & Tasks, Git Sync, Daily Runs, Domain Status, Triage, and Skill Library — each pinnable, with theme (slate/midnight/paper/mist) and density settings persisted in `localStorage`.

## How to run it

Static site, no build: open `index.html` directly in a browser, or serve the repo root with any static file server. In production it's served via GitHub Pages from the `main` branch root.

## Conventions

- **Never hand-edit `index.html`.** It's a rendered artifact; direct edits get overwritten (and possibly flagged as reverting to a "retired monolith") the next time ops-hub republishes. Content and layout changes belong in the ops-hub source workspace.
- Git history here is almost entirely automated "Daily republish" commits from the ops-hub reconcile loop (multiple passes per day), not manual development commits — that's expected and not a sign of repo neglect.
