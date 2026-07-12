# AGENTS — slide-decks

This repo is **documentation and slide decks — there is no application
source code.** No build step, no package manager, no tests to run. Each
top-level folder (`ai-dlc/`, and any added later) is one self-contained
Reveal.js deck: an `index.html`, its own `README.md`, and supporting
assets. Nothing outside those folders changes except this file and the
shared skill below.

## Editing a deck, or adding a new one

Every deck follows the same conventions: Reveal.js, dark/light theme via
CSS variables, Iconify icons (never emoji), Monaco-style code editor
panels, plain colorful HTML/CSS diagrams, simple-English copy, and a
single `DECK_CONFIG` block per deck driving a global footer with dynamic
page numbers and per-slide hide/show via `data-hidden="true"`.

The full rules and a starter template live in
`.claude/skills/slide-deck/SKILL.md` (mirrored at
`~/.claude/skills/slide-deck/SKILL.md` for use in any repo) — read that
before editing a deck or starting a new one. Do not invent a different
visual style or a different footer/pagination mechanism per deck; a new
deck starts from `.claude/skills/slide-deck/template.html`, not from
copying and stripping down an existing one.

## What this repo is not

No `src/`, no `backend/`, no `frontend/` — if a change here starts
looking like application code, it belongs in whatever project the deck
is narrating (e.g. [`agent-job-matcher`](https://github.com/senthilsweb/agent-job-matcher)
for `ai-dlc/`), not in this repo.
