# AGENTS — ai-dlc

This repo is **documentation and a slide deck — there is no application
source code.** No build step, no package manager, no tests to run. The
only thing that changes here is `index.html` (a single self-contained
Reveal.js presentation) and its supporting markdown notes.

## Editing the deck

`index.html` follows the author's standard slide-deck conventions:
Reveal.js, dark/light theme via CSS variables, Iconify icons (never
emoji), Monaco-style code editor panels, plain colorful HTML/CSS
diagrams, simple-English copy, and a single `DECK_CONFIG` block driving
a global footer with dynamic page numbers and per-slide hide/show via
`data-hidden="true"`.

The full rules and a starter template live in
`.claude/skills/slide-deck/SKILL.md` (mirrored at
`~/.claude/skills/slide-deck/SKILL.md` for use in any repo) — read that
before editing slides or adding new ones. Do not invent a different
visual style or a different footer/pagination mechanism for this deck.

## What this repo is not

No `src/`, no `backend/`, no `frontend/` — if a change here starts
looking like application code, it belongs in
[`agent-job-matcher`](https://github.com/senthilsweb/agent-job-matcher)
(the reference implementation this deck narrates), not in this repo.
