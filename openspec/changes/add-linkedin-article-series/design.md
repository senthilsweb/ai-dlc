# Design — `add-linkedin-article-series`

## Source material (facts only from these; no invented numbers)

| Source | What it supplies |
|---|---|
| `agent-job-matcher/README.md` | surfaces table, endpoints, tech stack, quick start, env vars |
| `agent-job-matcher/openspec/` (ADR 0001, change folders) | two-LLM invariant, graphify rationale, demo-stack scope |
| `agent-job-matcher/GRAPH_REPORT.md` | 451 nodes · 900 edges · 20 communities · 46 files ~77.5k words |
| `ai-dlc/index.html` (deck) | 3 phases / 7 ceremonies, 11 Bolts / 62 UoW / 135 evals, Bolt 10 story (7 UoW, 13 evals, email-vs-URL bug), Arize trace (9.58 s total, 8.78 s LLM ≈ 92%), Inception Gate (6 questions), status-line lifecycle |

## Style model — templrgo `content/blog`

Copied conventions (see the skill for the full codified list):

- YAML frontmatter: `title`, `slug`, `description`, `date` (ISO 8601),
  `published`, `type: blog`, `category`, `author`, `sort_order`, `tags`.
- H1 restates the title; short punchy intro before the first H2;
  "Why?" section early; tables for enumerable facts; fenced code for
  anything runnable; an honest "a word on..." aside (real bug, real
  trade-off) — never a cleaned-up retelling; "What's next"; a runnable
  CTA; sign-off; "Related reading" links last.

## File layout

```
articles-draft/
├── README.md                                  # series index + publish checklist
├── part-1-one-core-four-doors.md              + part-1-promo.md
├── part-2-specs-not-vibes.md                  + part-2-promo.md
├── part-3-anatomy-of-a-bolt.md                + part-3-promo.md
├── part-4-the-llm-never-scores.md             + part-4-promo.md
├── part-5-stop-burning-tokens-on-grep.md      + part-5-promo.md
└── part-6-ai-did-the-typing.md                + part-6-promo.md
```

Promo posts are separate files (not a section inside the article) so
each can be pasted into LinkedIn unedited.

## Cross-cutting decisions

1. **Demo link** (revised 2026-07-12, owner): the playground is
   hosted live at `jobmatch.nathansweb.com` on a deliberately cheap
   GPT model. Every article's CTA leads with the live link and offers
   `docker compose up` as the air-gapped / own-keys / own-model path.
   Part 1 keeps the `<!-- TODO(owner): demo video/GIF -->` slot.
2. **Series navigation**: every article opens with `Part n of 6` and a
   linked series list (`[LINK-PART-n]` placeholders until published);
   Part 6 doubles as the full recap/index.
3. **`published: false`** on all drafts; flipping it is the owner's
   per-article publish act (mirrors the hand-edited openspec status
   line — nothing promotes itself).
4. **Author** byline: `Senthilnathan (senthilsweb)`.
5. **Tone**: templrgo blog voice — confident, concrete, first person
   where it's genuinely the owner's experience; every claim traceable;
   admits limits (no hosted demo, no auth, frontend deliberately
   deferred).
