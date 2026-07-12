---
name: article-writing
description: Write or edit blog articles, documentation pages, and LinkedIn promo posts in the author's house style, modeled on the templrgo project's content/blog and content/docs corpus — YAML frontmatter, concrete numbers over adjectives, tables for enumerable facts, one honest aside per article, runnable CTAs, and a short hook-first promo post per article. Use whenever the user asks to draft, revise, or review an article, blog post, docs page, or LinkedIn post/series in this repo (articles-draft/) or any repo following this style.
user-invocable: true
---

# article-writing — my standard blog / docs / promo style

Modeled on and copied from the templrgo project's `content/blog` and
`content/docs` corpus (e.g. `introducing-knowledge-graph.md`,
`about-cv-guide.md`). One markdown file per piece. Promo posts are
separate files so they paste into LinkedIn unedited.

## Blog article frontmatter (required, this order)

```yaml
---
title: "Readable Title — Subtitle If It Earns One"
slug: kebab-case-stable-forever
description: One sentence, ~25 words, states the concrete payload — used for OG/meta, no clickbait
date: 2026-07-12T00:00:00Z
published: false        # flipped to true only when actually published
type: blog
category: Announcements | Engineering | Methodology | Series
author: Senthilnathan (senthilsweb)
sort_order: 10          # series position × 10
tags: [lowercase, kebab-case, 5-to-9-of-them]
---
```

## Docs page frontmatter (the smaller schema)

```yaml
---
title: "Feature Guide"
description: "Complete reference for X — what it covers, in one sentence."
weight: 6               # ordering within the docs section
---
```

Docs live in numbered section folders (`01-overview/`, `03-user-guide/`,
`04-developer/`); user guide and developer guide are separate pages,
never merged.

## Article structure (in order)

1. `# H1` restating the title.
2. **Cold open** — 2–3 sentences delivering the payload immediately
   ("We are shipping…", "The LLM never scores."). No throat-clearing,
   no "In today's fast-paced world".
3. **A "Why?" section early** — the problem in plain English, with the
   question the reader is actually asking in italics.
4. **Body H2s** — short, concrete ("What's in v1.4", "How it works
   (the 60-second tour)"). Tables for enumerable facts; fenced code
   for anything runnable; numbered lists only for real sequences.
5. **One honest aside** — a real bug, wrong first attempt, or
   deliberate limitation, told straight ("The first pass used indigo
   buttons — a leftover from an early storyboard."). Never a
   cleaned-up retelling; this section is what makes the piece credible.
6. **"What's next"** — bulleted, honest about what is not built.
7. **Runnable CTA** — the actual command or link, in a code block.
8. **Sign-off** — one line, em-dash + name.
9. **`## Related reading`** — bold-linked list with a one-clause
   description each. Always last.

## Voice rules

- Concrete numbers over adjectives: "135 evals", "9.58 seconds",
  "≤50 KB" — never "extensive", "blazing fast", "lightweight".
- Short declarative sentences for the big claims. One idea per
  paragraph; 1–3 sentence paragraphs.
- Bold the load-bearing noun on first appearance, not for emphasis.
- First person plural for team work, first person singular only when
  it is genuinely one person's experience or decision.
- Every claim traceable to the source repo/deck; a plan is written as
  a plan ("Phase 2 will…"), never as a shipped fact.
- No emoji in articles. No rhetorical questions except the italicized
  reader-question in the Why section.

## LinkedIn promo post (one per article, separate `-promo.md` file)

- ≤180 words, no markdown headings — LinkedIn renders plain text.
- Line 1 is the hook and must survive alone: it is all the feed shows
  before "…see more". A number or a contrarian claim beats a topic
  statement.
- Short line-broken paragraphs (1–2 sentences each), one blank line
  between them.
- One `[LINK]` placeholder for the article URL, near the end.
- 3–5 hashtags on the final line, camelCase multiword
  (`#PydanticAI #AIEngineering`).
- No fabricated engagement bait ("Agree?"), no "I'm humbled/excited to
  announce". The article's best fact is the post.

## Series conventions

- Every part opens with `Part n of 6` (or series length) and a linked
  list of all parts; unpublished parts use `[LINK-PART-n]`
  placeholders, replaced as each publishes.
- Shared CTA block verbatim in every part, so any entry point promotes
  the same repos/demo.
- The final part doubles as the recap and full index of the series.
