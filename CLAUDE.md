# Tsotoshi Workshop

A one-page portfolio that shows off tsotoshi's small browser games and apps. Visitors can browse the projects, then press Play/Open or view the source. Live at https://tsotoshi.github.io/tsotoshi-projects/.

## Tech stack

- Plain HTML, CSS and JavaScript, all inside `index.html`. There are no frameworks, no npm packages and no build step.
- Google Fonts: Bricolage Grotesque, Figtree and JetBrains Mono.
- Hosting: GitHub Pages serves the `main` branch, so pushing to `main` publishes the site within about a minute.
- Each project lives in its own repo under github.com/tsotoshi and is hosted separately (GitHub Pages, or Vercel for TravelTrax). This site only links to them.

## Commands

- Install: nothing to install.
- Run locally: open `index.html` in a browser, or run `python3 -m http.server` and visit http://localhost:8000.
- Test: there are no automated tests yet. Check changes by opening the page in a browser in both light and dark mode, at phone and desktop widths.
- Build: none. The files in the repo are exactly what gets published.
- Check the live deploy: `gh api repos/tsotoshi/tsotoshi-projects/pages/builds/latest --jq .status` (it reports `built` when the deploy is done).

## Project layout

- `index.html`: the whole site (page, styles and script).
- `shots/`: project screenshots, 960×600 JPGs named after each repo in kebab-case (e.g. `ff7-flappy.jpg`).
- `README.md`: a short public description.

## How the page works

- Every project card is built from the `PROJECTS` list near the bottom of `index.html`. To add or change a project, edit that list, not the HTML.
- Fields: `name`, `kind` ("game" or "app"), `status` ("live" or "wip"), `genre`, `created` (ISO date the project was started), `shot` (path in `shots/`, or `null` for a placeholder), `desc`, `keys` (list of `[key, action]` pairs; can be empty), `play` (live URL, or `null` to hide the button) and `repo`.
- Cards are sorted newest first by `created`, so the order of the list doesn't matter.
- Screenshots are shown at 2:1 and cropped from the top, so the bottom of each image gets cut off.
- Browsers keep images for up to 10 minutes. When you replace a screenshot, raise the `?v=` number on its `shot` path (e.g. `shots/traveltrax.jpg?v=3` to `?v=4`) so visitors see the new one.
- All text goes through `esc()` before it's added to the page. Keep that for any new field.
- Colors are CSS variables on `:root`. The dark-mode values appear twice: once in the `prefers-color-scheme: dark` block and again in `:root[data-theme="dark"]`. Always change both blocks together.
- To take a screenshot of a live project: `"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --hide-scrollbars --window-size=960,600 --screenshot=out.png <url>`. Add `--force-dark-mode` for dark mode. Then convert it with `sips -s format jpeg out.png --out shots/<name>.jpg`.

## Rules

- Explain changes to me in plain English — I'm still learning.
- Work in small steps; one feature at a time.
- Run tests before saying a task is done.
- Ask before adding new libraries or deleting files.
- Never put passwords, API keys, or secrets in code or in this file.
- When I say "wrap up": update the Current status section below, then commit and push everything to main, and confirm it's on main.

## Current status

_Last updated: 2026-11-10_

- Done: The site lists all 8 projects (Midgar Flap, TravelTrax, The Collection, Midnight Jelly, Range Day, Connect Four, Crack the Safe, Shopping & Returns Tracker). Has a light/dark switch and Games/Apps filters. This session added Midgar Flap and TravelTrax (with a dark-mode dashboard screenshot) and rewrote this CLAUDE.md.
- In progress: Nothing.
- Next: Add a screenshot and live link for Shopping & Returns Tracker once it's published.
- Decisions/notes: The TravelTrax screenshot is its dark-mode dashboard in demo mode. To retake it, run that app locally with `npm run dev` and no Supabase keys. Midgar Flap is labelled as a fan work not affiliated with Square Enix.
