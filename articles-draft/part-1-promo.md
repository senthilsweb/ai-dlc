I shipped the same AI agent four ways — CLI, REST API, Python package, and chat — from one core. It's live right now: jobmatch.nathansweb.com

The agent compares a resume against job postings and returns evidence-grounded fit reports: a 100-point score computed by pure code, exact resume quotes as proof, and a ready-to-send cover letter.

The part I care about: multi-surface isn't multi-codebase. The MCP server is a pure bridge. The chat service is a thin SSE adapter. Every door hits the same tested core.

Air-gapped or want your own model? docker compose up gives you the visual playground, branded API docs, and an embeddable chat widget — add your keys and start working.

All open source, MIT, production-grade. Part 1 of a 6-part series on how it was built (specs, evals, traces — the works).

[LINK]

#AIEngineering #MCP #OpenSource #GenAI #Agents
