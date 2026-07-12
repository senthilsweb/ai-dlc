# Proposal: LinkedIn article series (6 parts) + article-writing skill

> Status: **IMPLEMENTED** (2026-07-12) — all six article drafts and
> their promo posts written to `articles-draft/`; article-writing
> skill added; `AGENTS.md` updated. Pending: owner review of every
> draft, then per-article publish to LinkedIn (each publish flips
> that article's `published:` flag), then **verified** + archive.
> Revision: 2 (owner, 2026-07-12): live hosted playground at
> `jobmatch.nathansweb.com` (cheap GPT model) added to every CTA and
> to Part 1's body; `docker compose up` repositioned as the
> air-gapped / own-keys path; Part 3 "Why" section rewritten for
> clarity.
> Owner: @senthilsweb

## Why

`agent-job-matcher` is finished enough to talk about: a production-grade,
MIT-licensed, multi-surface GenAI agent built 100% through the AI-DLC
methodology this repo teaches. The training deck (`ai-dlc/index.html`)
already tells the story to a classroom; nothing tells it to LinkedIn.
A six-part article series promotes both repos — the product and the
methodology — with the live demo (`docker compose up`) and source code
as the call to action in every part.

This repo is the right home: `AGENTS.md` already declares it a
documentation-only repo, and the articles narrate the same project the
`ai-dlc/` deck narrates.

## What changes

1. **`articles-draft/`** gains the full series — six articles plus one
   short LinkedIn promo post per article, all in templrgo's
   `content/blog` markdown style (YAML frontmatter, H1, tables, code
   blocks, honest asides, "Related reading"), plus a `README.md` series
   index with the publishing checklist.
2. **Series order** (owner decision, this conversation): lead with the
   demo, close with the personal story —
   | Part | Working title | Angle |
   |---|---|---|
   | 1 | One Core, Four Doors | the showcase — surfaces, demo, repo |
   | 2 | Specs, Not Vibes | AI-DLC + spec-driven, for eng leaders |
   | 3 | Anatomy of a Bolt | ceremonies, evals, rubrics, traces |
   | 4 | The LLM Never Scores | Pydantic AI typed multi-model agents |
   | 5 | Stop Burning Tokens on Grep | graphify + Arize observability |
   | 6 | AI Did the Typing | first-person finale + series recap |
3. **`.claude/skills/article-writing/SKILL.md`** — a new repo skill
   codifying the blog/docs writing conventions, modeled on and copied
   from the templrgo project's `content/blog` and `content/docs`
   corpus (frontmatter schemas, tone, structure) plus LinkedIn promo
   post rules. Mirrors how the existing `slide-deck` skill works.
4. **`AGENTS.md`** — updated: the repo now contains articles as well
   as decks; points writers at the new skill.

## Non-goals

- No hosted public demo in this change — every article links the
  one-command `docker compose up` demo and leaves a marked `TODO`
  slot for a demo video/GIF the owner records before publishing.
- No publishing automation; LinkedIn publishing is manual, per part.
- No changes to `agent-job-matcher` itself.

## Acceptance

- Every article: valid frontmatter (`published: false` until the owner
  publishes), 800–1,400 words, only facts verifiable in
  `agent-job-matcher`, its `openspec/`, or the `ai-dlc/` deck — every
  number (bolts, evals, trace timings, graph size) traceable to source.
- Every article ends with the same CTA block (both repos + demo) and
  series navigation.
- Every promo post: ≤180 words, hook in line one, no fabricated claims,
  3–5 hashtags, a `[LINK]` placeholder for the published article URL.
- Skill file follows the existing `slide-deck` SKILL.md format
  (frontmatter: `name`, `description`, `user-invocable: true`).
