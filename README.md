# slide-decks

Reveal.js slide decks, one per top-level folder, all built to the same
house style: dark-navy/cyan theme with full light-mode support, Iconify
icons (never emoji), Monaco-style code panels, plain colorful HTML/CSS
diagrams, simple-English copy, and a dynamic hide-a-slide + auto-renumbering
footer. No application source code lives in this repo — it's documentation
and decks only.

## Decks

- **[`ai-dlc/`](ai-dlc/)** — *AI-DLC In Practice: agent-job-matcher.* Follows
  the live, end-to-end build of
  [`agent-job-matcher`](https://github.com/senthilsweb/agent-job-matcher)
  through the AI-Driven Development Lifecycle. See
  [`ai-dlc/README.md`](ai-dlc/README.md).

## The shared skill

Every deck here follows `.claude/skills/slide-deck/SKILL.md` — the rules for
theme, icons, code panels, diagrams, copy, and the `DECK_CONFIG` /
`data-hidden` / `data-section` mechanism each deck's `index.html` uses for
its footer and page numbers. Start a new deck by copying
`.claude/skills/slide-deck/template.html` into a new top-level folder here,
not by copying an existing deck. The same skill is also installed at
`~/.claude/skills/slide-deck/` for use in any repo, and mirrored here so the
convention travels with this repo specifically.

## Adding a new deck

1. `mkdir <deck-name>` at the repo root.
2. Copy `.claude/skills/slide-deck/template.html` to `<deck-name>/index.html`.
3. Follow `.claude/skills/slide-deck/SKILL.md` while building it.
4. Add a `<deck-name>/README.md` (see `ai-dlc/README.md` for the shape) and
   list the deck above.

## License

MIT
