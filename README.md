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

Three generations of the same idea, each one the "before" picture for the next gate:

1. **`talent-align`** — a vibe-coded prototype (pydantic-ai + Streamlit), built in an
   afternoon of chat, no process. Proved the idea works.
2. **`agents/job-matcher`** (Eve/TypeScript, in the
   [`ai-agents`](https://github.com/senthilsweb/ai-agents) monorepo) — the first
   AI-DLC governed rebuild: deterministic scoring in code, evidence-grounded
   extraction, evals-first, human-gated `.openspec.yaml` lifecycle. Proved the
   *design*.
3. **[`agent-job-matcher`](https://github.com/senthilsweb/agent-job-matcher)**
   (this deck's subject) — a standalone Python product rebuilt on that design,
   not on the Eve runtime: four access surfaces (CLI, REST, embeddable Python
   core, MCP + chat), exactly two LLM operations system-wide, eleven
   Construction bolts, and an eval suite restated as `pytest`.

## Slide overview

13 slides: cover · the story · three generations compared · ceremonies by
role · the AI-DLC cycle · a shared AI-DLC glossary (generic terms, reused
across this deck series) · the Inception gate's seven logged revisions ·
what a Bolt is (11 of them here) · architecture (two LLM calls, async
per-job fan-out) · evals as pytest (HARD/SOFT) · the security baseline ·
telemetry across four env-selected backends · running it four ways.

## Other files

- `AGENTS.md` — states this repo's nature (docs + slide deck, no
  application source code) and points at the slide-deck skill below.
- `.claude/skills/slide-deck/` — the author's standard Reveal.js
  deck-building conventions (theme, icons, code panels, diagrams, the
  hide/page-number mechanism) and a starter `template.html`. Also
  installed at `~/.claude/skills/slide-deck/` for use in any repo.
- `ceremonies-and-roles-eve-era.md` — the ceremony/role reference doc
  written for the Eve-era `job-matcher` build. Ceremony and role
  definitions still apply; runtime specifics (Eve sessions, subagents,
  `.ts` paths) predate `agent-job-matcher` and are kept as historical
  background, not as this repo's canonical narrative (that's `index.html`).

## Technology

- [Reveal.js 5.1.0](https://revealjs.com/) — presentation framework
- [Inter](https://fonts.google.com/specimen/Inter) — typography
- [Iconify](https://iconify.design/) (MDI set) — icons
- CSS custom properties for theming — the same navy/cyan house style used
  across this deck series (`ai-sdet-workbench`, `pii-classifier`)

## License

MIT
