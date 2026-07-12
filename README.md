# AI-DLC In Practice: agent-job-matcher

A [Reveal.js](https://revealjs.com/) teaching deck that follows the live,
end-to-end build of [`agent-job-matcher`](https://github.com/senthilsweb/agent-job-matcher)
through the **AI-Driven Development Lifecycle (AI-DLC)** — Inception,
Construction, Operations — using [OpenSpec](https://specs.md/)-style
`proposal.md` / `design.md` / `spec.md` / `tasks.md` gates.

This repo *is* the narrative, not the product: the product it narrates
lives at [github.com/senthilsweb/agent-job-matcher](https://github.com/senthilsweb/agent-job-matcher).

## View the deck

Open `index.html` in a browser, or serve it locally:

```bash
python -m http.server 8000     # or: npx serve .
```

Then navigate to `http://localhost:8000`.

- **Dark/Light theme toggle** — top-left button
- **Keyboard navigation** — arrow keys, Space, `F` (fullscreen), `O` (overview)
- **Hide a slide** — add `data-hidden="true"` to any `<section>`; it's pulled
  from navigation, the page count, and any PDF export, with nothing else to
  renumber by hand
- **PDF export** — via [Decktape](https://github.com/astefanutti/decktape)
  (not Reveal's built-in `?print-pdf`, which doesn't play well with this
  deck's fixed-position footer):
  ```bash
  python3 -m http.server 8000 &
  npx decktape reveal http://localhost:8000/index.html deck.pdf --size 1280x720
  ```

## The lineage this deck teaches

This is the second time this idea has been built properly. The first version
was a quick prototype — useful for proving the idea worked, but with
shortcuts (the AI graded its own answer, no automated tests, personal data
hard-coded) that don't belong in a real product.
[`agent-job-matcher`](https://github.com/senthilsweb/agent-job-matcher) (this
deck's subject) is a standalone Python product built the careful way from
scratch: four ways in (a command line, a web API, a Python import, and a
chat interface), a score computed by plain code rather than the AI, and 135
automated checks. See that repo's `openspec/project.md` for the full history.

## Slide overview

13 slides, all in plain English, no unexplained jargon: cover · what it does
· where the idea came from · how the work is organized · the AI-DLC cycle ·
a shared glossary (terms reused across this deck series) · the seven rounds
of plan changes before any code · the 11 build steps with their real test
counts, as a table · how it's put together · how it's tested · how it's kept
safe · a real trace of a real run, viewed in Arize AX · running it four ways.

## Other files

- `AGENTS.md` — states this repo's nature (docs + slide deck, no
  application source code) and points at the slide-deck skill below.
- `.claude/skills/slide-deck/` — the author's standard Reveal.js
  deck-building conventions (theme, icons, code panels, diagrams, the
  hide/page-number mechanism) and a starter `template.html`. Also
  installed at `~/.claude/skills/slide-deck/` for use in any repo.
- `assets/` — real screenshots used in the deck (the Arize AX trace on the
  "watching it run" slide).

## Technology

- [Reveal.js 5.1.0](https://revealjs.com/) — presentation framework
- [Inter](https://fonts.google.com/specimen/Inter) — typography
- [Iconify](https://iconify.design/) (MDI set) — icons
- CSS custom properties for theming — the same navy/cyan house style used
  across this deck series (`ai-sdet-workbench`, `pii-classifier`)

## License

MIT
