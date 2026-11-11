# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Tsotoshi Workshop: a single-page portfolio that links to tsotoshi's browser games and apps. It is served by GitHub Pages from `main` at https://tsotoshi.github.io/tsotoshi-projects/. Pushing to `main` deploys it.

There is no build step, package manager, linter or test suite. The whole site is `index.html` (inline CSS and JS) plus screenshots in `shots/`. To preview it, open `index.html` in a browser, or run `python3 -m http.server` and visit http://localhost:8000.

## How the page works

- **Data-driven cards.** Every project card is rendered from the `PROJECTS` array near the bottom of `index.html`. You add, edit or remove a project there, never in the HTML markup. Each entry has these fields:
  - `name`, `kind` (`"game"` | `"app"`), `status` (`"live"` | `"wip"`), `genre`
  - `created`: an ISO timestamp for when the project was started. Cards are sorted newest first, so the order of entries in the array doesn't matter.
  - `shot`: a path under `shots/`, or `null` to show a striped "screenshot coming soon" placeholder
  - `desc`, `keys` (a list of `[key, action]` pairs rendered as `<kbd>` hints; can be empty)
  - `play`: the live URL, normally `https://tsotoshi.github.io/<Repo>/`, or `null` to hide the Play/Open button. The button says "Play" for games and "Open" for apps.
  - `repo`: the GitHub URL for the Source button
- **Each project lives in its own repo** under github.com/tsotoshi and is deployed with that repo's own GitHub Pages. This repo only links to them.
- **Screenshots** are JPGs in `shots/` named after the repo in kebab-case. They are shown at a 2:1 aspect ratio with `object-fit: cover` anchored to the top, so the bottom of a taller image gets cropped.
- **Escaping.** `card()` passes every text field through `esc()` before putting it into `innerHTML`. Keep that in place for any new field.
- **Theming.** Colors are CSS custom properties on `:root`. The dark values are defined twice: once under `@media (prefers-color-scheme: dark)` with `:root:not([data-theme="light"])`, and again under `:root[data-theme="dark"]`. Change both blocks together. A small inline script in `<head>` applies the saved `localStorage.theme` before first paint so the page doesn't flash the wrong theme. The selected filter is also saved in `localStorage`, and every storage call is wrapped in try/catch.
