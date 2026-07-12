---
title: "Anatomy of a Bolt — Ceremonies, Evals, Rubrics, and Traces on a Real Feature"
slug: anatomy-of-a-bolt
description: One real Bolt dissected — 7 tasks, 13 evals written from the rubric before the code, one genuine bug they caught, and the Arize trace that closed the loop
date: 2026-07-12T00:00:00Z
published: false
type: blog
category: Series
author: Senthilnathan (senthilsweb)
sort_order: 30
tags: [ai-dlc, evals, rubrics, traces, arize, observability, testing, methodology]
---

# Anatomy of a Bolt

> **Production-Grade Agents, Built in the Open — Part 3 of 6**
> 1. [One Core, Four Doors]([LINK-PART-1]) · 2. [Specs, Not Vibes]([LINK-PART-2]) · 3. Anatomy of a Bolt (this article) · 4. [The LLM Never Scores]([LINK-PART-4]) · 5. [Stop Burning Tokens on Grep]([LINK-PART-5]) · 6. [AI Did the Typing]([LINK-PART-6])

Part 2 gave you the ledger: 11 Bolts, 62 tasks, 135 evals. This part
zooms into a single real Bolt — the cover-letter feature — and walks
every AI-DLC ceremony it passed through: the rubric that defined done,
the 13 evals written *before* the code, the genuine bug they caught,
and the production trace that closed the loop. Not a cleaned-up
retelling.

## Why?

Most writing about AI methodology stops at the diagram level — phases,
arrows, ceremony names — and never shows the artifacts a developer
actually touches. *What does "evals before code" look like in
practice, on one ordinary feature?* This article answers with the real
things: the rubric file that defined "done", the task checklist, the
pytest run, and the bug report — so you can judge the method by its
day-to-day mechanics, not its vocabulary.

## The ceremonies, in one pass

AI-DLC runs three phases — Inception, Construction, Operations — with
seven ceremonies across them. On this project they materialized as:

| Ceremony | Artifact in the repo |
|---|---|
| Intent | `proposal.md` — why this change exists |
| Inception Gate | six open questions settled before code (Bolt 0) |
| Design | `design.md` — the architecture, committed |
| Mob Construction | Bolts of Units of Work in `tasks.md` |
| Evals | `pytest backend` — the spec's rules, executable |
| Operations Review | traces in Arize AX, read by a human |
| Next Intent | the next change folder — the loop closes |

The vocabulary is Agile renamed for AI-speed work: a **Bolt** replaces
the sprint (hours or days, not weeks), a **rubric** replaces the
acceptance-criteria meeting, **evals** replace the test plan, and
**traces** replace the retro's anecdotes with data.

## Bolt 10, task by task

The feature: every job report ships a rendered cover letter built from
the LLM's typed paragraphs through a plain-text template. Seven Units
of Work:

1. Pull contact details from the resume with plain pattern-matching —
   no AI call, so a wrong guess is structurally impossible.
2. Write the default template, shipped with the package.
3. Fall back to that default when no custom template is supplied.
4. Wire the candidate's details into the letter step, computed once.
5. Write **13 new evals** — including fields missing on purpose.
6. Run once against a real model; read the actual output.
7. Re-run the whole suite clean: 109/109 at the time.

The 13 evals came straight from the rubric
([`backend/evals/rubrics.md`](https://github.com/senthilsweb/agent-job-matcher/blob/main/backend/evals/rubrics.md)):
8 on extracting contact details — including *"this field is genuinely
missing, don't invent it"* — and 5 on the rendered letter: default
template, operator override, and a grounding check that every detail
in the letter is a literal piece of the resume.

## The bug the evals caught

Here's the honest part. An email like `sam.lee@example.com` was briefly
misread as a website too — the URL pattern excluded what comes *after*
the `@`, not the name before it. Caught immediately by testing against
real examples, fixed by stripping emails from the text before hunting
for URLs, and logged as a dated **Correction** in the spec — not
silently rewritten. The missing-field evals and the grounding eval
existed *before* the Bolt was called finished; they weren't added
afterward to match whatever the code happened to do.

## Traces: the Operations Review ceremony

Every run leaves a real trace. One captured 2026-07-11 in **Arize AX**,
start to finish — 9.58 seconds:

| Step | Time |
|---|---|
| Fetch the job posting | 0.8 s |
| Ask the LLM what matches | 8.78 s |
| Score it & save the report | <0.1 ms |

92% of the run is waiting on the one LLM call. That single trace
settled a design argument permanently: there is nothing to optimize in
the scoring code, and any future latency work is model choice, nothing
else. That's what the Operations Review ceremony is *for* — replacing
"I think it's slow because…" with a picture.

The eval suite splits along the same line the traces reveal:

```bash
pytest backend -m "not live"   # offline: scoring, guards, schemas — free, seconds
pytest backend -m live         # real-model sweep: grounding, injection, fan-out
```

Fixtures are committed real-world captures — four job-description
snapshots, two genuine fetch failures, one adversarial prompt-injection
JD — so every eval reproduces after the postings close.

## What's next

- **Part 4** goes into the code: how Pydantic AI's typed outputs make
  "the LLM never scores" structurally true, not aspirationally true.

## Try it, read it, fork it

Everything is open source, MIT-licensed, and production-grade:

- **Source**: [github.com/senthilsweb/agent-job-matcher](https://github.com/senthilsweb/agent-job-matcher)
- **Methodology + training deck**: [github.com/senthilsweb/ai-dlc](https://github.com/senthilsweb/ai-dlc)
- **Live playground**: [jobmatch.nathansweb.com](https://jobmatch.nathansweb.com) — hosted demo, running a deliberately cheap GPT model
- **Air-gapped / your own models**: `docker compose up -d` — add your keys and start working

— Senthilnathan

## Related reading

- **[Part 2 — Specs, Not Vibes]([LINK-PART-2])** — the methodology this Bolt lives inside.
- **[Part 4 — The LLM Never Scores]([LINK-PART-4])** — the typed-agent implementation.
- **[The rubric file](https://github.com/senthilsweb/agent-job-matcher/blob/main/backend/evals/rubrics.md)** — acceptance criteria as an executable contract.
