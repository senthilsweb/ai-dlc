Every fresh AI coding session starts ignorant. It greps, reads, and re-derives the same cross-references — and bills you for the privilege.

My fix: CI regenerates a knowledge graph of the repo on every push — 451 nodes, 900 edges, 20 communities from ~77K words — at a token cost of exactly zero. Extraction is AST-based and deterministic. No LLM.

The part agents actually load: a ≤50 KB graph-index.json sized for a context window. One file-read and the agent knows the core abstractions — the graph found them by edge count (JobReport: 37 edges), not by anyone declaring them.

Same repo, other direction: runtime traces stream to Arize purely by setting env vars. Instrumentation is decorator-only — the scoring code contains zero telemetry calls.

Honest footnote included: 42% of graph edges are inferred at 0.65 confidence. It's a map, not ground truth.

Part 5 of 6, all open source.

[LINK]

#KnowledgeGraph #TokenOptimization #Observability #Arize #AIEngineering
