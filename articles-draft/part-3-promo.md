13 evals were written before the code. They caught a real bug the first day: an email address misread as a website URL.

That's what "evals before code" looks like on a Tuesday — not a diagram, a regex bug caught by a test that existed before the feature did. Fixed, and logged as a dated Correction in the spec. Never silently rewritten.

New in the series: one real Bolt of my AI-DLC build dissected end to end — 7 tasks, 13 evals from the rubric, the bug, and the Arize trace that closed the loop.

The trace settled an argument permanently: 9.58s per run, 8.78s of it waiting on the one LLM call. Scoring takes <0.1ms. There is nothing to optimize except model choice — and now that's a picture, not an opinion.

Part 3 of 6. Rubrics, evals, traces — every ceremony, on a real feature.

[LINK]

#Evals #AIDLC #Observability #Arize #AIEngineering
