# DESIGN.md

Direction for the atl2600 site. Read together with the antislop core
(`antislop.md`) and the UI skill: this file supplies the soul (identity,
palette, type, mood, dials); the filter decides what is allowed.

> Provenance: written by the agent from the existing brand signals in this
> repo (group name, audience, copy voice, old theme) plus the 2026-09-02
> audit of the MDwiki build below. The group maintainers should review and
> edit this file; it is the source of truth for future design work.

## Identity

atl2600 is the Atlanta chapter of 2600, a community of computer and
security enthusiasts in the DEF CON lineage. The number comes from the
2600 Hz touch-tone signal used by blue boxes: the group name is literally
a tone. The culture is terminal, phone-phreaking, CTF, "the only things
we byte are chips". This page is a community bulletin: it exists to tell
people when and where to show up, and where to hang out between meetings.

## Audience

Security engineers, CTF players, students, and curious newcomers in the
Atlanta area. They read terminals all day. They distrust polish and
marketing language. The page should feel like something a member wrote,
not like a vendor built it.

## Personality

- Plain-spoken and practical. The copy stays exactly as the members wrote
  it; the design gets out of its way.
- Technical without performing it: the terminal aesthetic comes from the
  group's actual heritage (tones, terminals, CTF), not from a costume.
- One quiet edge, not a neon rave.

## Design Read

> Reading this as: a community bulletin page for a local security group,
> in a terminal-inherited visual language, dial ENERGY 2 / RHYTHM 2 /
> MOTION 1.

- ENERGY 2: the page says hello with character (monospace voice, prompt
  headings, one amber accent) but the job is information, not spectacle.
- RHYTHM 2: consistent single-column reading flow with a few deliberate
  breaks (the meeting block is visually set apart from the link lists).
- MOTION 1: hover and focus states only. No loops, no scroll reveals.
  The page ships zero JavaScript.

## Palette

Two core colors plus one accent (R-29). No gradients, no glow, no orbs.

| Token | Hex | Role | Reason |
|---|---|---|---|
| `--bg` | `#101418` | page background | Near-black slate, not pure black: terminal-culture audience (R-21 legitimate dark reason: security/developer community), easier on the eyes than `#000`. |
| `--surface` | `#1a2026` | one elevated panel | The meeting details, the page's actual job, sits one level up. Only panel on the page; elevation is flat, done with the surface tone, not a shadow (R-12). |
| `--text` | `#e8e6e0` | body text | Warm off-white, 14.8:1 on bg. |
| `--muted` | `#9aa0a6` | secondary text | 7.0:1 on bg, still AAA. |
| `--line` | `#2a3138` | hairline borders | Structure without shadow. |
| `--accent` | `#ffb000` | single accent | Phosphor amber: a nod to 2600's signal-and-CRT heritage, and deliberately outside the blue/purple/cyan AI-default family (R-01). The color of every link on the page (links hover to `--text`), plus the prompt markers and focus outlines. |

Contrast (computed, WCAG): text/bg 14.8, muted/bg 7.0, accent/bg 10.1,
text/surface 13.2, muted/surface 6.2, accent/surface 9.0, bg-on-accent
10.1. All AA, most AAA.

## Typography

- Display/labels: monospace stack
  `ui-monospace, "Cascadia Code", "SF Mono", Menlo, Consolas, "Liberation Mono", monospace`.
  Reason (R-06): 2600's heritage is tones, terminals, and CTF boxes;
  monospace is the group's native voice, chosen for brand character, not
  as a generic "technical" costume. System stack only: no webfont payload,
  no single default library look (R-04 icon-lib logic applies to type too).
- Body: system sans stack
  `system-ui, -apple-system, "Segoe UI", Roboto, Helvetica, Arial, sans-serif`.
  Reason: paragraphs stay readable at bulletin length; the sans/mono
  contrast is the hierarchical device (R-31).
- Scale: one large moment (the wordmark), section heads in mono small-caps
  size (1.125rem, weight 700, no extreme tracking), body 1rem/1.6.
  No uppercase + wide letter-spacing labels (the R-06 tell).

## Layout

Single column, `max-width: 65ch`, centered. The composition follows the
content (R-05, C-3):

1. Header: wordmark `atl2600` + tagline "Your local 2600 connection.",
   anchor nav (About, Meetings, Friends, Events) plus the GitHub source link.
   Every nav item targets a section that exists on the page (R-24).
2. Notice banner: a one-line, temporary announcement at the top of
   `main`, above `#about`, set on an accent-yellow block with dark text.
   It carries a time-sensitive fact (a venue change for one month) that
   the regular `#meetings` copy does not. It is present only while the
   notice is true; when it is stale the line is removed, not left to rot.
   The yellow is `--accent`, the page's one deliberate accent used at the
   key moment: a solid accent block is the design's existing emphasis
   language (the accent is "the emphasis"), so no border, shadow, glow,
   uppercase label, or icon is added (R-01, R-06, R-09, R-12, R-13).
    Text on it is `--bg` at 10.1:1 (AA/AAA, table above). The banner
     carries one photo of the venue (`sandbox-location.png`) as a
    48px-tall thumbnail next to the text. Clicking it grows the same
    image to full content width in place: the thumbnail is an anchor to
    its own id, the `:target` state does the growing, and a
    "click to shrink" link (visible only while expanded) points back at
    the banner's id to release the target. It is the page's only
    stateful control and it is pure CSS, zero JS (R-26): the element
    changes only because the user acted, with no transition (MOTION 1).
    Links inside the accent block use `--bg` ink, and the focus outline
    is `--bg` too: the accent link treatment (yellow on dark) is
    invisible on yellow, and there is no second readable ink on the
    banner, so hover feedback is the pointer cursor. Still no link to
    `#meetings`: it would show the wrong venue for that month.
3. `#about`: the first section in `main`, explaining what 2600 is
    (community in the DEF CON lineage, the tone, the magazine it is
    based on, the Atlanta chapter forming in 1992) with a link to
    2600.org. It comes first among the sections to orient the reader
    before the page's job; like the other sections it carries the prompt
    marker and a nav item.
4. `#meetings`: the page's job. Set apart as the one `--surface` panel:
    in-person details, the venue in a real `<address>` element, the
    Discord invite as the action link. It is plain text (no box, no
    padding, no border) so the panel stays quiet; the accent link color
    is the only action treatment (R-12, R-31).
5. `#friends`: compact list of the local groups, the three dc groups
    plus Atlanta Women in Cyber, each with its real URL. dc404 carries
    more copy (it is the active one); the layout reflects that difference
    instead of four identical cards (R-14).
6. `#events`: B-Sides Atlanta, short.
7. Footer: one line, source link and the infosec.exchange/@atl2600
    account. No 4-column template footer (R-05).

No hero, no CTA pair, no logo bar, no bento, no fake terminal window,
no 3-step "how it works", no pricing. There is no product to demo, so
there is nothing to fake (R-38, C-5).

## Identity Motif

The prompt marker: section headings render as a terminal path
(`~/meetings`, `~/friends`, `~/events`) with the `~` in accent color, and
the wordmark carries a static block cursor (`▮`) that does not blink.
One gesture, repeated, specific to the group, zero motion. It is what
makes the page "atl2600" rather than "a dark site" (R-20, Part 3 lever).

## Dose Caps

- Glassmorphism: 0 (R-10).
- Glow: 0 (R-13). Nothing glows; the accent color is the emphasis.
- Shadow: 0. Elevation is the flat `--surface` step (R-12).
- Radius: 2px everywhere. Terminal windows are not rounded; a single
  small radius is the system (R-11).
- Icons: none. Feature labels and real URLs do the work; no icon library
  is imported (R-04).
- Arrows: none on links (R-08).
- Badges: none (R-09).
- Images: 1, the venue photo in the notice banner. A real, verifiable
  place shown as evidence, not decoration; it expands on click. No other
  imagery (R-22, C-5).

## Motion

MOTION 1. The only transitions are a 120ms color change on link/button
hover and focus. `prefers-reduced-motion: reduce` disables even that.
No element moves without the user. The one layout state on the page is
the notice photo, which grows or shrinks instantly on click via CSS
`:target` with no transition: it changes only because the user acted,
so it stays inside MOTION 1.

## Accessibility

- All text pairs meet WCAG AA (table above).
- Links: accent text, no underline, and the link text drops the protocol
  (`https://`); the full URL stays in `href`. Reason (R-31): the audience
  reads URLs natively, the protocol is noise, and the accent color is
  the page's single link signal, so an underline would fight it.
  Accepted trade-off: an inline link in running text (Kali) is then
  identified by color alone; the accent holds 10.1:1 on bg and 9.0:1 on
  the panel, and hover shifts it to `--text` as feedback.
- Visible focus: 2px `--accent` outline, 2px offset, on every interactive
  element; native keyboard order (R-32). Inside the accent banner the
  outline is `--bg` instead: an accent outline would be invisible on the
  accent background. The photo expand/shrink toggle is a pair of plain
  links, so Tab + Enter drives it; the "click to shrink" link is
  `display: none` (out of the tab order) until the photo is expanded.
- Single column, no fixed pixel widths, long URLs wrap
  (`overflow-wrap: anywhere`), tap targets >= 44px (R-03).
- Semantic landmarks: `header`, `nav`, `main`, `section`, `address`,
  `footer`. One `h1` (the wordmark).

## Copy

The members' words are the design. No rewriting, no marketing polish, no
buzzwords, no em dashes (R-02, R-16). If a fact changes (a new venue, a
new link), edit the text in `index.html` directly and keep this file in
sync if the design decisions change.

---

## Audit of the previous design (MDwiki v0.6.2, 2026-09-02)

The old site was an MDwiki shell: `index.html` was a 337 KB empty
`<div id="md-all">` that fetched `index.md` at runtime and rendered it
with jQuery 1.8.3 + Bootstrap 3.0.0 + highlight.js 7.3 + ColorBox, all
inlined, in the Bootswatch "cyborg" (inverse) theme.

| # | Finding | Rule | Disposition |
|---|---|---|---|
| 1 | Content requires JavaScript; without it the page is a noscript notice. A text-only community page should not. | R-26, C-2 | Rebuilt as pure static HTML, zero JS. |
| 2 | 337 KB of inlined 2013-era JS (jQuery 1.8.3 has known CVEs; highlight.js and ColorBox are unused by this content). | C-1 | Removed; nothing replaces them. |
| 3 | Palette is a stock 2013 Bootswatch theme applied wholesale; no identity, no written reason. | R-01, R-29, R-31 | Replaced by the palette above, derived from the group's identity. |
| 4 | Default Bootstrap type; no typeface decision. | R-06 | Mono/sans split with written reasons. |
| 5 | Tool-generated chrome: auto TOC sidebar, dropdown side menu, anchor glyphs on every heading, fork-me ribbon. Structure came from the generator, not the content. | R-05, C-3 | Replaced with content-driven sections; nav links only what exists (R-24). |
| 6 | `favicon.png` referenced but absent from the repo (broken 404 asset). | C-2 | Replaced with `favicon.svg` (motif: the 2600 tone as a sine wave). |
| 7 | No `DESIGN.md`, `README.md`, or `AGENTS.md`. | R-37, repo hygiene | All three added. |
| 8 | What was good and is preserved: real, member-written copy; real, verifiable links; no invented stats, logos, or testimonials. | R-17, R-18, R-36 | Content carried over verbatim. |
