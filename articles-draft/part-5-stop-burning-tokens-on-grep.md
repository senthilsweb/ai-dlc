---
title: "Stop Burning Tokens on Grep — A CI-Built Knowledge Graph plus Env-Activated Observability"
slug: stop-burning-tokens-on-grep
description: Graphify regenerates a 451-node knowledge graph of the repo on every push — zero LLM cost — with a ≤50 KB index slice for AI coding agents, while decorator-only instrumentation streams runtime traces to Arize
date: 2026-07-12T00:00:00Z
published: false
type: blog
category: Series
author: Senthilnathan (senthilsweb)
sort_order: 50
tags: [knowledge-graph, graphify, token-optimization, arize, observability, opentelemetry, ci]
---

# Stop Burning Tokens on Grep

> **Production-Grade Agents, Built in the Open — Part 5 of 6**
> 1. [One Core, Four Doors]([LINK-PART-1]) · 2. [Specs, Not Vibes]([LINK-PART-2]) · 3. [Anatomy of a Bolt]([LINK-PART-3]) · 4. [The LLM Never Scores]([LINK-PART-4]) · 5. Stop Burning Tokens on Grep (this article) · 6. [AI Did the Typing]([LINK-PART-6])

This project watches AI from two directions. Runtime observability
watches the LLM *inside* the product — that's the Arize trace from
Part 3. This article adds the other direction: a CI-generated
**knowledge graph** that keeps the AI agents *building* the product
from burning tokens rediscovering the codebase every session. Both are
open, both are in the repo, and the graph costs **zero LLM tokens** to
build.

## Why?

Every fresh AI coding session starts ignorant. It greps, reads,
re-derives the same cross-references — *which schemas does `/analyze`
touch? what calls `run_analysis()`?* — and each rediscovery bills you
in tokens and time. The repo is 46 files and ~77,500 words; large
enough (the graph report itself makes this call) that structure beats
search.

## Graphify: the map, rebuilt by CI

On every push to `main`, a GitHub Actions workflow regenerates and
commits three artifacts at the repo root:

| Artifact | What it is |
|---|---|
| `graph.json` | the full graph — **451 nodes, 900 edges, 20 communities** |
| `graph-index.json` | a **≤50 KB** slice, sized for an LLM's context window |
| `graph-manifest.json` | provenance — what was built, from what, when |

Extraction is deterministic — AST parsing plus community clustering,
no LLM involved. The graph report literally logs `Token cost: 0 input
· 0 output`. An agent (or a human) starts a session by loading the
50 KB index instead of grepping, and immediately knows the god nodes:
`JobReport` (37 edges), `JobAnalysis` (28), `extract_resume_text()`
(24). Those *are* the core abstractions — the graph found them by
degree count, not by anyone declaring them.

The CI wiring has the boring-but-load-bearing details right: a
`[skip graphify]` commit marker prevents the workflow from triggering
itself, failures open a tracking issue instead of blocking `main`, and
a weekly cron catches drift. The graph files are CI-owned — the repo's
conventions forbid editing them by hand.

Worth noting: this wasn't retrofitted. The graphify change was specced
and wired in during the project's first days, on the explicit argument
(recorded in its own `openspec/` proposal) that adopting the machinery
is cheap while the repo is small and painful later — the pipeline was
lifted from a prior project where it had already earned its keep.

## The other direction: watching the product run

Runtime observability follows two rules from the repo's engineering
conventions, and they're the reason it stays clean:

**Instrumentation is aspect-oriented.** Tracing and timing attach only
via decorators — `@traced`, `@timed`. Core function bodies contain
zero telemetry calls. You can read the scoring logic without stepping
over span boilerplate.

**Backends are env-activated, never code-selected.** Structured JSON
logs are always on. Everything else joins the fan-out purely by
setting that backend's own documented env vars:

```bash
ARIZE_SPACE_ID=... ARIZE_API_KEY=...        # Arize AX
PHOENIX_COLLECTOR_ENDPOINT=...              # Arize Phoenix
OTEL_EXPORTER_OTLP_ENDPOINT=...             # any OTLP collector
OPENOBSERVE_URL=...                         # OpenObserve, plain REST
```

No `if backend ==` anywhere. Vendor SDK imports are allowed only
inside the sink layer, and a telemetry delivery failure is logged and
swallowed — it never fails a run. That's how the 9.58-second Arize
trace in Part 3 existed at all: someone set two env vars, and every
run started leaving a map of itself.

## A word on what the graph is not

First, scope: the graph maps the repository for the agents building
it; it never touches the product's runtime. Nothing in the served API
loads `graph.json` — the two observability directions in this article
share a repo and a philosophy, not a process.

Second, confidence. The graph report is candid about its own: 58% of edges are
extracted directly, 42% are *inferred* at an average confidence of
0.65. It's a map, not ground truth — good enough to orient an agent in
one file-read, not good enough to replace reading the code it points
to. Also honest: the workflow supports an optional LLM semantic pass
if you give it an API key; this repo deliberately runs without one,
because free-and-deterministic beats slightly-richer-and-billed for
this purpose.

## What's next

- **Part 6** closes the series: what the human actually did in all of
  this — the Inception Gate calls, the hand-edited status lines, the
  corrections — and the full series recap.

## Try it, read it, fork it

Everything is open source, MIT-licensed, and production-grade:

- **Source**: [github.com/senthilsweb/agent-job-matcher](https://github.com/senthilsweb/agent-job-matcher)
- **Methodology + training deck**: [github.com/senthilsweb/ai-dlc](https://github.com/senthilsweb/ai-dlc)
- **Live playground**: [jobmatch.nathansweb.com](https://jobmatch.nathansweb.com) — hosted demo, running a deliberately cheap GPT model
- **Air-gapped / your own models**: `docker compose up -d` — add your keys and start working

— Senthilnathan

## Related reading

- **[Part 3 — Anatomy of a Bolt]([LINK-PART-3])** — the runtime trace this article's env vars produced.
- **[GRAPH_REPORT.md](https://github.com/senthilsweb/agent-job-matcher/blob/main/GRAPH_REPORT.md)** — the CI-generated graph report, god nodes and all.
- **[RUNBOOK.md](https://github.com/senthilsweb/agent-job-matcher/blob/main/RUNBOOK.md)** — workflows, releases, and the graphify pipeline.
