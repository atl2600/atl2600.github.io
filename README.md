# atl2600

The website for [atl2600](https://atl2600.org), the Atlanta chapter of
2600: when and where we meet, who we meet with, and what is coming up.

## What this is

A single hand-written HTML page. No build step, no JavaScript, no
framework, no webfonts, no external requests. Edit `index.html` in a
browser and you see the site.

## Requirements

Nothing to install. Any browser renders it.

## Development

- `index.html` is the entire site. Edit it directly.
- `DESIGN.md` is the source of truth for design direction (palette,
  type, layout, dials) and records the reason for every major decision.
  Read it before changing the look, and keep it in sync if a decision
  changes.
- The meeting/chat/event text is written by group members. Do not
  rewrite it; update facts in place.
- There are no tests. Verification: open the page in a browser, check
  the anchors work, check it on a narrow window, and compare text
  contrast against the values tabulated in `DESIGN.md`.

## Project structure

| Path | What it is |
|---|---|
| `index.html` | The whole site. |
| `favicon.svg` | Sine-wave favicon (the 2600 tone motif). |
| `DESIGN.md` | Design direction + audit of the previous build. |
| `AGENTS.md` | Instructions for coding agents. |
| `datadup/2019-04/` | GPG-signed checksum files for a 2019 video data drop. Archive data, not site code. Leave it alone. |
| `CNAME` | GitHub Pages custom domain (atl2600.org). |

## Deployment

Push to `main`. GitHub Pages publishes the branch and serves
`index.html` at `https://atl2600.org`.
