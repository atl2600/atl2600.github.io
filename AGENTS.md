# AGENTS.md

Instructions for coding agents working in this repository.

## Project

Static website for atl2600.org (Atlanta chapter of 2600), served by
GitHub Pages from the `main` branch. The site is one hand-written HTML
file with no build step and no JavaScript.

## Ground rules

- `index.html` is the site. Edit it directly; there is nothing to build.
- `DESIGN.md` is the design source of truth. Read it before changing
  anything visual. Every visual decision in it has a written reason;
  keep new decisions to the same standard and update the file.
- The prose in `index.html` (meetings, friends, events) is written by
  group members. Never rewrite it for style. Update facts only when the
  user asks.
- No JavaScript, no frameworks, no webfonts, no external requests, no
  CSS frameworks. The page must keep working with JS disabled (it
  always can, because it uses none).
- `datadup/` is archived GPG-signed data, not site code. Do not modify
  or delete it.
- `CNAME` points at the live domain. Do not change it.

## Verification

There is no test runner. Before calling a change done:

1. Open `index.html` in a browser (desktop and a narrow mobile width).
2. Confirm every nav anchor resolves to a section that exists.
3. Confirm contrast holds against the table in `DESIGN.md`
   (all pairs WCAG AA or better).
4. For UI work, run the antislop Delivery Gate (see below) and report
   its PASS/FAIL status.

## Deployment

Push to `main`; GitHub Pages serves the branch at atl2600.org.

<!-- antislop:start -->
## antislop
For UI, copy, people, mobile layout, or code comments work, read `DESIGN.md` for direction, then the antislop core and the skill for the task. In this environment they live at:
- Core: `/home/user/.config/opencode/skills/antislop/SKILL.md`
- UI / visual: `/home/user/.config/opencode/skills/antislop-ui/SKILL.md`
- Copy & text: `/home/user/.config/opencode/skills/antislop-copywriting/SKILL.md`
- People: `/home/user/.config/opencode/skills/antislop-human/SKILL.md`
- Mobile / responsive: `/home/user/.config/opencode/skills/antislop-layoutmobile/SKILL.md`
- Code comments: `/home/user/.config/opencode/skills/antislop-code/SKILL.md`
Before starting, ask the user when antislop applies: during the work, or after it is done.
<!-- antislop:end -->
