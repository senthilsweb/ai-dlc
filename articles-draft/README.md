# articles-draft — "Production-Grade Agents, Built in the Open" (6-part series)

LinkedIn article series about [agent-job-matcher](https://github.com/senthilsweb/agent-job-matcher)
and the [AI-DLC](https://github.com/senthilsweb/ai-dlc) methodology it
was built with. Written per `.claude/skills/article-writing/SKILL.md`;
scoped by `openspec/changes/add-linkedin-article-series/`.

## The series (publish in this order)

| Part | File | Angle | Audience |
|---|---|---|---|
| 1 | `part-1-one-core-four-doors.md` | The showcase — one agent core, every surface, live demo | everyone |
| 2 | `part-2-specs-not-vibes.md` | AI-DLC + spec-driven development, the what and why | eng leaders |
| 3 | `part-3-anatomy-of-a-bolt.md` | Every ceremony in practice — evals, rubrics, traces | practitioners |
| 4 | `part-4-the-llm-never-scores.md` | Typed multi-model agents with Pydantic AI | AI engineers |
| 5 | `part-5-stop-burning-tokens-on-grep.md` | Graphify knowledge graph + Arize observability | AI engineers |
| 6 | `part-6-ai-did-the-typing.md` | First-person finale — the human/AI split + series recap | everyone |

Order rationale: lead with the demo (what), then the method (how), then
the deep dives (why it's solid), close with the personal story and full
recap. Each `part-n-promo.md` is the matching LinkedIn feed post —
paste as-is.

## Publish checklist (per part)

1. Review the draft; fix anything off-voice.
2. Part 1 only: record the demo video/GIF (`TODO(owner)` slot marked).
3. Publish on LinkedIn as an article.
4. Replace `[LINK]` in that part's promo and `[LINK-PART-n]` in every
   other file with the live URL.
5. Flip that article's `published: false` → `true`.
6. Post the promo to the feed, ~1 week apart per part.
7. After Part 6: flip the openspec proposal to VERIFIED and archive.
