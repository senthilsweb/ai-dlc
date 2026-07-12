---
title: "Specs, Not Vibes — Building a Production Agent with AI-DLC"
slug: specs-not-vibes-ai-dlc
description: How a production-grade AI agent was built through 11 Bolts, 62 tasks, and 135 evals under AI-DLC — a spec-driven lifecycle where every change is a committed proposal, design, task list, and executable spec
date: 2026-07-12T00:00:00Z
published: false
type: blog
category: Series
author: Senthilnathan (senthilsweb)
sort_order: 20
tags: [ai-dlc, spec-driven, methodology, openspec, evals, ai-engineering]
---

# Specs, Not Vibes

> **Production-Grade Agents, Built in the Open — Part 2 of 6**
> 1. [One Core, Four Doors]([LINK-PART-1]) · 2. Specs, Not Vibes (this article) · 3. [Anatomy of a Bolt]([LINK-PART-3]) · 4. [The LLM Never Scores]([LINK-PART-4]) · 5. [Stop Burning Tokens on Grep]([LINK-PART-5]) · 6. [AI Did the Typing]([LINK-PART-6])

The agent from Part 1 was built through **62 tasks and 135 evals across
11 Bolts** — every one of them written down, committed, and checkable in
the repo before the code that satisfies it. No vibe-coding, no "the AI
wrote it and it seems fine." The methodology is called **AI-DLC** (the
AI-Driven Development Lifecycle), and this article is the what and why;
Part 3 walks the ceremonies in detail.

## Why?

AI pair-programming has an uncomfortable failure mode: the code appears
faster than your ability to judge it. *If the AI does the typing, what
stops the project from drifting into something nobody specified?* The
answer AI-DLC gives: specs the AI must satisfy, evals that make those
specs executable, and a human who owns every promotion decision. AI
moves fast inside the fence; humans build the fence.

## One folder, no dashboard

Every non-trivial change in the repo starts life as a folder:

```
openspec/changes/add-job-matcher-cli/
├── proposal.md      # why + status line + revision log
├── design.md        # the architecture
├── tasks.md         # 11 Bolts, task by task
└── specs/.../spec.md # 16 rules, one per eval
```

The state of a change is one hand-edited line at the top of its
proposal: `> Status: IMPLEMENTED`. It only moves one way — proposed →
approved → implemented → verified → archived — and **a person edits it,
every time**. Nothing promotes itself. Anyone (human or AI agent) can
see where everything stands with one command, `/openspec-status`. No
Jira, no YAML pipeline, no separate dashboard to rot.

## Bolts, not sprints

AI-DLC renames Agile's ceremonies for AI-speed work. The unit of
construction is a **Bolt**: a short burst of "Mob Construction" — a
handful of Units of Work finished in hours or days, not the weeks a
sprint takes — each one finished *and tested* before the next begins.

The real ledger from this build:

| Bolt | What it built | Tasks | Evals |
|---|---|---|---|
| 0 | Inception Gate — six open questions settled, no code yet | 8 | — |
| 1 | Scoring math + the shape of every piece of data | 8 | 37 |
| 2 | Reading resumes, fetching postings safely | 3 | 22 |
| 3 | The one AI call + the CLI | 9 | 8 |
| 4 | The REST API | 4 | 12 |
| 5 | Telemetry fan-out | 5 | 8 |
| 6 | Resume → JSON Resume conversion | 4 | 10 |
| 7 | MCP server for Claude Desktop | 3 | 5 |
| 8 | The chat bridge | 6 | 9 |
| 9 | Live-model verification | 5 | 11 |
| 10 | Cover letter generation | 7 | 13 |
| **11 Bolts** | | **62** | **135** |

Two details worth pausing on. Bolt 0 shipped **zero code** — the
Inception Gate settled six open questions (scoring ownership, document
parsing strategy, LLM count, and so on) before construction started.
And of the 135 evals, all but Bolt 9's 11 run offline — no model, no
network, free forever. Only Bolt 9 deliberately spends money to verify
against a real LLM before anything ships.

## The circle, not the line

AI-DLC is a loop: what Operations Review teaches becomes the Next
Intent. Proof it actually loops: the day after the main build was
verified, a fourth change folder appeared —
`add-demo-stack-and-playground`, its own five Bolts, specced and
implemented the same way. That's the demo stack you saw in Part 1.

## A word on bending the rules

Not every change got the full ceremony. The CI/knowledge-graph change
was owner-directed and implemented in the same commit as its approval —
recorded exactly that way in its status line, with a dated revision
log. The methodology's real rule isn't "never move fast"; it's **never
move silently**. A shortcut you write down is a decision; a shortcut
you don't is drift.

## What's next

- **Part 3** zooms all the way in: every AI-DLC ceremony, a single Bolt
  dissected task by task, the rubric that generated its evals, and a
  real bug the evals caught.
- The methodology itself — vocabulary, ceremonies, worked example — is
  a free training deck in the [ai-dlc repo](https://github.com/senthilsweb/ai-dlc),
  with this project as its running example.

## Try it, read it, fork it

Everything is open source, MIT-licensed, and production-grade:

- **Source**: [github.com/senthilsweb/agent-job-matcher](https://github.com/senthilsweb/agent-job-matcher)
- **Methodology + training deck**: [github.com/senthilsweb/ai-dlc](https://github.com/senthilsweb/ai-dlc)
- **Live playground**: [jobmatch.nathansweb.com](https://jobmatch.nathansweb.com) — hosted demo, running a deliberately cheap GPT model
- **Air-gapped / your own models**: `docker compose up -d` — add your keys and start working

— Senthilnathan

## Related reading

- **[Part 1 — One Core, Four Doors]([LINK-PART-1])** — what got built.
- **[Part 3 — Anatomy of a Bolt]([LINK-PART-3])** — the ceremonies in practice.
- **[openspec/ in the repo](https://github.com/senthilsweb/agent-job-matcher/tree/main/openspec)** — read the actual specs this article describes.
