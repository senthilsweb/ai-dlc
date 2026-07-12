---
name: slide-deck
description: Build or edit a Reveal.js slide deck in the author's personal house style — dark-navy/cyan theme with full light-mode support, Iconify or Lucide icons (never emoji), Monaco-style code editor panels, colorful HTML/CSS diagrams (no chart libraries), simple plain-English copy, and a dynamic hide-a-slide + auto-renumbering footer. Use whenever the user asks to create a slide deck, presentation, or Reveal.js deck, or to edit one that already follows this style (e.g. a file with data-section attributes and a DECK_CONFIG block). Also covers exporting the deck to PDF with Decktape.
user-invocable: true
---

# slide-deck — my standard Reveal.js deck style

One self-contained `index.html` per deck. No build step, no framework, no
`package.json` — open the file in a browser or serve it with any static
file server. A repo that only contains decks like this has **no source
code**: treat it as documentation, not an application.

Start every new deck from `template.html` in this skill's folder — copy
it, don't rewrite it from memory. It already has the full CSS system, the
dynamic footer/pagination script, the theme toggle, and one example of
every reusable component described below.

## The rules

**Reveal.js.** Version 5.x from `cdn.jsdelivr.net`, `black` base theme
overridden by a custom `<style>` block of CSS variables. `width: 1280,
height: 720`. Linear deck only — no vertical slide stacks, no
`autoSlide`. Transition is `'fade'`. `controls`, `progress`, and `hash`
all stay on, so slides are keyboard-navigable and deep-linkable. This is
the "normal flow" rule: predictable, one-directional, nothing fancy
enough to disorient a live audience.

**Icons, never emoji.** Every icon is an `<iconify-icon icon="...">`
element (loaded from `code.iconify.design`) — Material Design Icons
(`mdi:*`) is the default set already wired into the template, but any
Iconify collection works, including `lucide:*` when a thinner, more
minimal icon language fits better. Do not type an emoji character
anywhere in slide content, including as a bullet marker or decoration —
emoji render inconsistently across platforms and fonts (some render in
full color even inside otherwise monochrome UI, which breaks the theme).
If you need a checkmark, gate symbol, warning triangle, and so on, use
the matching icon (`mdi:check`, `mdi:gate`, `mdi:alert`) instead of the
Unicode emoji glyph. Plain typographic symbols that are not emoji — →, ·,
▸, ↻ — are fine.

**Dark and light theme, both real.** Every color in slide markup is a
`var(--color-*)` reference, never a literal hex value — that is what
makes the light-mode toggle actually work instead of leaving white text
on a white background. The toggle button (top-left, fixed position)
flips `data-theme` on `<html>` and persists the choice to
`localStorage` under the key in `DECK_CONFIG.themeStorageKey`; an inline
script in `<head>` reads it before first paint so there's no flash. When
you add a new color token, add it to both the `:root` block (dark
defaults) and the `[data-theme="light"]` override block — never only one.

**Code panels look like a code editor.** Wrap code in `.editor-window` >
`.editor-titlebar` (three colored dots + a filename/command label) >
`.editor-body` (monospace, dark background). The editor background stays
dark **even in light theme** — a code panel is a window into an editor,
not a themed content card, so it should not flip color with the rest of
the deck. Use the `.cmt` / `.cmd` / `.acc` / `.ok` / `.bad` span classes
inside `.editor-body` for lightweight pseudo-syntax-highlighting (muted
comment gray, cyan for a command, amber for something to notice, green
for success, red for failure) instead of a real syntax highlighter — it
reads clearly from the back of a room without adding a dependency.

**Diagrams are plain colorful HTML/CSS, not a charting library.** The
template ships a small component library — reuse it rather than
inventing new patterns per slide:

| Component | Use it for |
|---|---|
| `.flow-row` + `.flow-card` (numbered, cyan/amber/green accents) | A left-to-right process: input → transform → output |
| `.twocol` + `.panel` | Any "diagram on the left, explanation on the right" slide |
| `.data-table` | Structured comparisons (before/after, options, specs) |
| `.step-list` (numbered circles) | An ordered list of steps or rules |
| `.emphasis-box` (cyan/green/amber variants) | The one sentence you want remembered from the slide |
| `.pill-tag` | Short keyword badges, e.g. on a cover slide |

A custom diagram (a cycle, a pipeline, a grid) is fine when nothing above
fits — build it from `position: absolute`/`grid` boxes styled with the
same color tokens, the same way the components above are built. Keep it
simple enough to point at and narrate out loud; if a diagram needs its
own explanation to explain the diagram, simplify it.

**Language: simple English, no jargon.** Write for someone encountering
the topic for the first time. Short sentences. Spell out an acronym the
first time it appears on a given slide. Prefer a concrete example over
an abstract description. If a technical term is unavoidable, define it
in the same breath, not in a footnote.

**Hide a slide without renumbering anything.** Add `data-hidden="true"`
to any `<section>` to pull it out of the deck — a script at the bottom of
`<body>` removes `data-hidden` sections from the DOM *before*
`Reveal.initialize()` runs, so a hidden slide is excluded from
navigation, the progress bar, the page count, and a Decktape export, all
at once. Un-hide by deleting the attribute (or setting it to `"false"`).
Nothing else needs to change — page numbers recompute from whichever
slides are actually left.

**One global footer, not one per slide.** Do not paste a `<div
class="slide-footer">` into every `<section>` — that was the old
pattern and it means editing 13 places to change a GitHub link. Instead:
give each `<section>` a `data-section="Short Label"` attribute (shown at
the left of the footer, next to the deck title), and let the single
`DECK_CONFIG` object at the top of the main `<script>` block drive
everything else — deck title, GitHub URL, website URL, theme storage
key. The footer element itself is built once in JS and stays fixed at
the bottom of the viewport across every slide; its page-number text
(`N / total`) updates on Reveal's `slidechanged` event by reading the
current slide's computed `data-page`. This is the "global variable, edit
at the top, dynamic" requirement — change `DECK_CONFIG` once, every
slide's footer updates.

## Workflow for a new deck

1. Copy `template.html` to the target repo as `index.html` (or another
   name the user asks for).
2. Edit the `DECK_CONFIG` object near the bottom: `title`, `githubUrl`,
   `websiteUrl`, `themeStorageKey` (make the storage key unique per deck
   so two decks open in the same browser don't share a theme setting).
3. Set `<title>` in `<head>` to the deck's real title.
4. Build slides using the component table above. Give every `<section>`
   a `data-section="..."` attribute. Never write a per-slide footer or a
   hardcoded page number.
5. If a slide is a draft or a cut, mark it `data-hidden="true"` rather
   than deleting it — it's easy to bring back later.
6. Open the file directly in a browser (or `python3 -m http.server` from
   the deck's folder) and click through it before calling it done —
   check both themes with the toggle.

## Exporting to PDF (Decktape)

Decktape drives a real Chromium instance and captures one PDF page per
slide by walking the deck through Reveal's own API — it does **not**
rely on Reveal's CSS print-media mode, so `position: fixed` elements
(the theme toggle, the footer) render correctly on every page, and
hidden slides are simply absent because they were removed from the DOM
before Reveal even started.

```bash
# serve the deck locally first
python3 -m http.server 8000 &

npx decktape reveal http://localhost:8000/index.html deck.pdf \
  --size 1280x720
```

## Also available as

This same skill lives in three places — keep them in sync if you change
the rules or the template:

- `~/.claude/skills/slide-deck/` (this copy) — every project, every repo
- `<repo>/.claude/skills/slide-deck/` — mirrored into decks-only repos so
  the convention travels with the repo itself
- claude.ai Skills (Settings → Capabilities → Skills) — paste this
  file's contents in manually; there's no CLI/API path to publish there,
  so that copy has to be updated by hand when this one changes
