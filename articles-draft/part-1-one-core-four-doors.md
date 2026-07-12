---
title: "One Core, Four Doors — Shipping the Same AI Agent as CLI, REST, MCP Tool, and Chat"
slug: one-core-four-doors
description: One embeddable agent core, four production surfaces — CLI, REST API, Python package, and chat over MCP — demoable in one docker compose command
date: 2026-07-12T00:00:00Z
published: false
type: blog
category: Series
author: Senthilnathan (senthilsweb)
sort_order: 10
tags: [agents, mcp, fastapi, pydantic-ai, open-source, genai, multi-surface]
---

# One Core, Four Doors

> **Production-Grade Agents, Built in the Open — Part 1 of 6**
> 1. One Core, Four Doors (this article) · 2. [Specs, Not Vibes]([LINK-PART-2]) · 3. [Anatomy of a Bolt]([LINK-PART-3]) · 4. [The LLM Never Scores]([LINK-PART-4]) · 5. [Stop Burning Tokens on Grep]([LINK-PART-5]) · 6. [AI Did the Typing]([LINK-PART-6])

I built an AI agent that compares a resume against job postings and
returns **evidence-grounded, deterministically scored** fit reports.
Then I shipped the same agent four ways: a CLI, a REST API, an
embeddable Python package, and a chat assistant that drives it through
MCP. One core, four doors — and the whole thing is open source, MIT,
and live right now at
[jobmatch.nathansweb.com](https://jobmatch.nathansweb.com), or on your
own machine with a single `docker compose up`.

<!-- TODO(owner): 60–90s demo video/GIF here before publishing -->

## Why?

Every agent demo you see is a chat window. But real users arrive from
different directions: *an engineer wants a terminal command, a system
wants an API, a Python service wants an import, and everyone else
wants to just talk to it.* Building four apps is how you end up with
four bugs per feature. The alternative: build the intelligence once,
make every surface a thin adapter.

The product itself is deliberately simple to explain: give it a resume
(PDF, DOCX, or text) and one or more job posting URLs; get back a
ranked report per job — a 100-point score (required skills 40 /
preferred 20 / experience 20 / domain 20), a match band, the exact
resume quotes that justify every skill match, and a ready-to-send
cover letter. The LLM extracts evidence; **pure code computes every
score**. More on why that matters in Part 4.

## The four doors

| Surface | Entry | Protocol |
|---|---|---|
| CLI | `jobmatch analyze --resume me.pdf --job <url>` | terminal; persists full artifacts to `runs/<timestamp>/` |
| REST | `POST /analyze`, `POST /resume/jsonresume` | FastAPI; stateless, typed JSON array |
| Python | `from job_matcher import run_analysis` | in-process, for embedding in other agents |
| Chat | MCP server + agent service | stdio for Claude Desktop; REST/SSE bridge for any web chat widget |

Every door hits the same `job_matcher` core: fetch → extract → score.
The CLI is [Typer](https://typer.tiangolo.com/), the API is
[FastAPI](https://fastapi.tiangolo.com/), and the chat path is a Node
[MCP](https://modelcontextprotocol.io/) server that is a *pure bridge*
to the REST API — it contains no intelligence of its own.

The chat door is the interesting one, protocol-wise. Claude Desktop
speaks to the MCP server over **stdio**. A browser chat widget can't
do stdio, so a small agent service exposes `POST /chat/stream` over
**SSE** and hosts the orchestration LLM, which calls the same MCP
tools internally. Two transports, one tool surface, zero duplicated
logic.

## Try it live — or run it air-gapped

The hosted playground is at
**[jobmatch.nathansweb.com](https://jobmatch.nathansweb.com)**: upload
a resume, add job links, get visual fit reports. It runs on a
deliberately cheap GPT model so a free public demo stays affordable.

Prefer your own model, your own keys, or no internet dependency at
all? The same stack is one command:

```bash
git clone https://github.com/senthilsweb/agent-job-matcher && cd agent-job-matcher
cp .env.example .env        # add your OpenAI or Anthropic key
docker compose up -d
# playground    http://localhost:3011  — upload a resume, add job links, get visual fit reports
# openapi-docs  http://localhost:3012  — browsable, branded API reference
# chat-demo     http://localhost:8091  — the embeddable chat widget
```

The playground renders each job report as a compact visual card — the
score breakdown, evidence quotes, and match band — instead of a chat
transcript. The API docs app serves a branded reference over the live
OpenAPI spec. And that spec isn't decorative: it's generated from the
FastAPI app and attached to **every GitHub release**, and an offline
test fails the build if any endpoint ships without a description and
fixture-sourced examples.

## A word on what's *not* here

Honesty section. The hosted playground runs the cheapest viable GPT
model, because every analysis there spends *my* API key — judge output
quality by running the stack locally against a stronger model of your
choice. There's no sign-in yet either: a deliberate, recorded decision
in the project's specs, not an oversight.
And a visual playground existed only as raw JSON until one week ago;
the demo stack you see was itself a spec-driven change, built the day
after the core shipped.

## What's next

- **Part 2** covers *how* this was built: 11 Bolts, 62 tasks, and 135
  evals under a spec-driven methodology called AI-DLC — with every
  spec committed in the repo for you to read.
- On the product side: sign-in, rate limits, and a stronger default
  model for the hosted playground are on the list as usage grows.

## Try it, read it, fork it

Everything is open source, MIT-licensed, and production-grade:

- **Source**: [github.com/senthilsweb/agent-job-matcher](https://github.com/senthilsweb/agent-job-matcher)
- **Methodology + training deck**: [github.com/senthilsweb/ai-dlc](https://github.com/senthilsweb/ai-dlc)
- **Live playground**: [jobmatch.nathansweb.com](https://jobmatch.nathansweb.com) — hosted demo, running a deliberately cheap GPT model
- **Air-gapped / your own models**: `docker compose up -d` — add your keys and start working

— Senthilnathan

## Related reading

- **[Part 2 — Specs, Not Vibes]([LINK-PART-2])** — the AI-DLC methodology behind this build.
- **[agent-job-matcher README](https://github.com/senthilsweb/agent-job-matcher#readme)** — architecture diagram and quick start.
- **[ADR 0001](https://github.com/senthilsweb/agent-job-matcher/blob/main/openspec/adr/0001-agent-service-chat-bridge.md)** — why exactly two LLM operations exist.
