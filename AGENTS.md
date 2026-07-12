# AGENTS — slide-decks & articles

This repo is **documentation, slide decks, and article drafts — there
is no application source code.** No build step, no package manager, no
tests to run. Each top-level deck folder (`ai-dlc/`, and any added
later) is one self-contained Reveal.js deck: an `index.html`, its own
`README.md`, and supporting assets. `articles-draft/` holds blog /
LinkedIn article drafts and their promo posts. Non-trivial changes go
through `openspec/changes/<name>/` first (proposal → design → tasks →
spec), the same lifecycle
[`agent-job-matcher`](https://github.com/senthilsweb/agent-job-matcher)
follows. Nothing outside those folders changes except this file and
the shared skills below.

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

## Writing an article, docs page, or promo post

Everything under `articles-draft/` (and any future `content/` folder)
follows the house writing style codified in
`.claude/skills/article-writing/SKILL.md` — templrgo-style YAML
frontmatter (`content/blog` schema for articles, the smaller
`title`/`description`/`weight` schema for docs pages), concrete
numbers over adjectives, one honest aside per article, a runnable CTA,
and a separate ≤180-word hook-first `-promo.md` file per article for
LinkedIn. Read that skill before drafting or editing any article. All
drafts ship with `published: false`; the owner flips the flag when a
piece actually publishes.

## What this repo is not

No `src/`, no `backend/`, no `frontend/` — if a change here starts
looking like application code, it belongs in whatever project the deck
is narrating (e.g. [`agent-job-matcher`](https://github.com/senthilsweb/agent-job-matcher)
for `ai-dlc/`), not in this repo.
