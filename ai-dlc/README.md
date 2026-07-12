# AI-DLC In Practice: agent-job-matcher

A [Reveal.js](https://revealjs.com/) teaching deck that follows the live,
end-to-end build of [`agent-job-matcher`](https://github.com/senthilsweb/agent-job-matcher)
through the **AI-Driven Development Lifecycle (AI-DLC)** — Inception,
Construction, Operations — using [OpenSpec](https://specs.md/)-style
`proposal.md` / `design.md` / `spec.md` / `tasks.md` gates.

This deck *is* the narrative, not the product: the product it narrates
lives at [github.com/senthilsweb/agent-job-matcher](https://github.com/senthilsweb/agent-job-matcher).
This folder is one deck inside the [`slide-decks`](https://github.com/senthilsweb/slide-decks)
repo — see the root [README](../README.md) for the others.

## View the deck

From this folder, open `index.html` in a browser, or serve it locally:

```bash
cd ai-dlc
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

16 slides, in plain English but using AI-DLC's real vocabulary throughout —
this deck's whole point is teaching that vocabulary, not hiding it: cover ·
what it does · where the idea came from · the three phases and seven
ceremonies · the AI-DLC cycle · who's in the mob (three people carry it —
Product Owner, AI Engineer, QA — everyone else is one of them directing an
AI agent) · a shared glossary · the six rounds of plan revisions before any
code · how the project is tracked (the real `openspec/` folder and its
status line — no YAML file) · all 11 Bolts with their real task and eval
counts, as a table · one Bolt opened up completely (tasks, evals, and a real
bug) · how it's put together · evals and the rubric that grades them · how
it's kept safe · a real trace of a real run, viewed in Arize AX · running it
four ways.

## Other files

- `assets/` — real screenshots used in the deck (the Arize AX trace on the
  "watching it run" slide).
- `archive/` — earlier drafts of `index.html`, kept for reference rather
  than lost when the deck gets rewritten.

This deck follows the shared `.claude/skills/slide-deck/` convention and
`AGENTS.md` one level up, at the repo root — see there for the house style
and for how to add another deck alongside this one.

## Technology

- [Reveal.js 5.1.0](https://revealjs.com/) — presentation framework
- [Inter](https://fonts.google.com/specimen/Inter) — typography
- [Iconify](https://iconify.design/) (MDI set) — icons
- CSS custom properties for theming — the same navy/cyan house style used
  across this deck series (`ai-sdet-workbench`, `pii-classifier`)

## License

MIT
