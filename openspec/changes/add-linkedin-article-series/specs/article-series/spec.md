# Spec — article series rules

Every rule is checkable by reading the files; no tooling required.

## Requirement: Article structure

Every `articles-draft/part-*.md` (non-promo) SHALL:

- carry complete templrgo-blog frontmatter (`title`, `slug`,
  `description`, `date`, `published`, `type: blog`, `category`,
  `author`, `sort_order`, `tags`) with `published: false` until the
  owner publishes that part;
- open with `Part n of 6` and the linked series list;
- run 800–1,400 words of body;
- contain at least one table or fenced code block;
- contain one honest aside (a real bug, limit, or trade-off — never
  only wins);
- end with the shared CTA block (agent-job-matcher repo, ai-dlc repo,
  the live playground at `jobmatch.nathansweb.com`, and the
  `docker compose up` air-gapped path) followed by series navigation.

#### Scenario: A part is drafted

- GIVEN a new `part-n-*.md`
- WHEN it is reviewed against this spec
- THEN every bullet above holds, and every number in the body is
  traceable to `agent-job-matcher`, its `openspec/`, `GRAPH_REPORT.md`,
  or the `ai-dlc/` deck.

## Requirement: Promo posts

Every `part-n-promo.md` SHALL be pasteable into LinkedIn unedited:
≤180 words, hook as the first line (visible before "…see more"),
line-broken short paragraphs, 3–5 hashtags, exactly one `[LINK]`
placeholder for the article URL, no markdown headings.

#### Scenario: Publishing a part

- GIVEN the owner publishes part n on LinkedIn
- WHEN the article URL exists
- THEN `[LINK]` in `part-n-promo.md` and `[LINK-PART-n]` in every
  other file are replaced, and part n's `published:` flips to `true`.

## Requirement: No invention

No article or promo SHALL state a metric, quote, or capability that
does not exist in the source material listed in `design.md`. A wish
("hosted demo") is written as a plan or TODO, never as fact.
