---
title: "AI Did the Typing. I Did the Thinking. Here's the Split."
slug: ai-did-the-typing
description: The first-person close of the series — what a human actually contributes when AI writes the code, why the second attempt at this idea succeeded, and the full six-part recap
date: 2026-07-12T00:00:00Z
published: false
type: blog
category: Series
author: Senthilnathan (senthilsweb)
sort_order: 60
tags: [ai-dlc, ai-engineering, career, methodology, retrospective, open-source]
---

# AI Did the Typing. I Did the Thinking.

> **Production-Grade Agents, Built in the Open — Part 6 of 6**
> 1. [One Core, Four Doors]([LINK-PART-1]) · 2. [Specs, Not Vibes]([LINK-PART-2]) · 3. [Anatomy of a Bolt]([LINK-PART-3]) · 4. [The LLM Never Scores]([LINK-PART-4]) · 5. [Stop Burning Tokens on Grep]([LINK-PART-5]) · 6. AI Did the Typing (this article)

This is the second time I've built this idea. The first attempt worked,
roughly, the way most AI-assisted side projects work: fast start, fog
of half-finished pieces, no way to say what was *done*. The second
attempt — the one this series described — shipped as a production-grade
system with 135 evals and a committed spec for every change. Same idea,
same person, same AI assistance. The variable was the method.

## Why?

Every "AI built my app" post triggers the same question: *then what
are you for?* After this build I can answer it concretely, because
AI-DLC forces the split into the open. The AI typed nearly everything.
Here is what it could not do.

## What the human actually did

**Settled the questions no one asked.** Bolt 0 shipped zero code. The
Inception Gate settled six open questions — who owns scoring, how
documents get parsed, how many LLM calls exist — before construction
started. An AI will happily build any of the wrong versions; deciding
which version is *right* was the job.

**Wrote the rubric before wanting the feature.** The 13 cover-letter
evals from Part 3 existed before the code because a human decided what
"done" meant first — including the eval for a contact field that's
*missing on purpose*. Evals-after-code test what the code does;
evals-before-code test what you meant.

**Moved every status line by hand.** proposed → approved → implemented
→ verified → archived. Five words, edited manually, every time.
Nothing in the pipeline promotes itself, which means every promotion
is a human accepting responsibility on the record.

**Read the traces and the outputs.** Bolt 9 exists solely to spend a
little money running the real model and *reading what came back*. The
Arize trace that showed 92% of runtime in one LLM call ended a
performance debate a human was about to start in the wrong place.

**Logged the mistakes as mistakes.** The email-parsed-as-URL bug is in
the spec as a dated Correction. The rule that made the whole thing
work: never move silently. A recorded shortcut is a decision; an
unrecorded one is drift.

## The split, honestly

Three roles carried this project, and only one of them types fast. The
AI did the construction — at a pace no human matches. A human supplied
intent, taste, and judgment at the gates. And the evals stood between
them as the referee neither side can charm. Remove any one of the
three and you get a familiar failure: no AI, too slow; no human,
confidently wrong; no evals, unverifiable either way.

What surprised me most: the method didn't slow the AI down. Bolts run
hours-to-days. The day after the main build verified, a whole new
five-Bolt change (the demo stack from Part 1) went from proposal to
implemented. Discipline compounds speed once the fence is built.

## The series, complete

| Part | The claim it defends |
|---|---|
| [1 — One Core, Four Doors]([LINK-PART-1]) | multi-surface isn't multi-codebase |
| [2 — Specs, Not Vibes]([LINK-PART-2]) | 62 tasks, 135 evals, one hand-edited status line |
| [3 — Anatomy of a Bolt]([LINK-PART-3]) | evals before code, on a real feature, with a real bug |
| [4 — The LLM Never Scores]([LINK-PART-4]) | prompt injection with no schema field to land in |
| [5 — Stop Burning Tokens on Grep]([LINK-PART-5]) | a 451-node repo map at zero token cost |
| 6 — this one | what the human is for |

## What's next

- The playground is now hosted live at
  [jobmatch.nathansweb.com](https://jobmatch.nathansweb.com); sign-in,
  rate limits, and a stronger default model are queued as usage grows.
- The AI-DLC training deck (the classroom version of this series, with
  this project as the worked example) is free in the
  [ai-dlc repo](https://github.com/senthilsweb/ai-dlc).
- The loop keeps turning: whatever Operations Review teaches next
  becomes the Next Intent.

## Try it, read it, fork it

Everything is open source, MIT-licensed, and production-grade:

- **Source**: [github.com/senthilsweb/agent-job-matcher](https://github.com/senthilsweb/agent-job-matcher)
- **Methodology + training deck**: [github.com/senthilsweb/ai-dlc](https://github.com/senthilsweb/ai-dlc)
- **Live playground**: [jobmatch.nathansweb.com](https://jobmatch.nathansweb.com) — hosted demo, running a deliberately cheap GPT model
- **Air-gapped / your own models**: `docker compose up -d` — add your keys and start working

If any part of this series was useful, the repos are the real payload
— fork them, run the evals, steal the method.

— Senthilnathan

## Related reading

- **[Part 1 — One Core, Four Doors]([LINK-PART-1])** — start of the series, and the demo.
- **[AI-DLC training deck](https://github.com/senthilsweb/ai-dlc)** — three phases, seven ceremonies, one real project.
- **[openspec/ in the repo](https://github.com/senthilsweb/agent-job-matcher/tree/main/openspec)** — every decision this series described, in the original.
