# GovScraper Mockups

Static HTML mockups for the GovScraper member portal — for internal review and coder hand-off.

**Live:** https://mendsourcing.github.io/gs-mockups/

## Mockups

| Path | Description |
| --- | --- |
| [`/notifications.html`](https://mendsourcing.github.io/gs-mockups/notifications.html) | Email Preferences page — per-notification toggles, MAXX-only visibility, always-on transactional list |

## How to add a new mockup

1. Drop a self-contained `.html` file into the root of this repo.
2. Add a card to `index.html` linking to it.
3. `git add . && git commit -m "add <name> mockup" && git push` — GitHub Pages redeploys automatically (~30-60s).

## Notes

- All mockups are static HTML — no build step, no dependencies.
- Match the GovScraper design tokens (Manrope + DM Sans, `#1B6CA8` accent, `#0F172A` headings, `#F1F5F9` surface-2, etc.).
- These are references, not production code.
