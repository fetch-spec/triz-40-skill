---
name: triz-40-questions
description: Use when you're stuck on a design, product, or process problem, a trade-off won't resolve, or the discussion keeps going in circles. Walks all 40 TRIZ inventive principles as questions, honestly tags each result, and ends with a short list of proposals, their risks, and the cheapest tests.
---

# TRIZ 40 Questions

TRIZ's 40 inventive principles (Altshuller) are the recurring moves behind many inventions. Asking all 40 against a real problem forces angles you'd never think of. The discipline is in asking every one and being honest when one doesn't fit.

## When to use
- You're stuck on a design, product, engineering, data, or process problem.
- Two goals seem to fight each other (improving one makes another worse).
- The team keeps circling the same few ideas.

Not for simple lookups or problems with a known answer.

## 1. State the problem
Before any question, write:
- **System:** what it is and what it does.
- **Must improve:** the thing that has to get better.
- **Core contradiction:** "We need to improve **[X]**, but doing so seems to worsen **[Y]**."
- **Known facts vs assumptions:** list what is measured or sourced. Label everything else `ASSUMPTION`.
- **Decisions already made:** list constraints and choices already settled, so you can spot rediscoveries later.

If you can't state a contradiction, stop and clarify with the person who owns the problem.

## 2. Walk all 40, in order
Use [questions.md](questions.md). For every principle:
- Give **one concrete suggestion** that applies to this problem, **or** write **"nothing useful here"**. Never force an idea. A forced idea is noise.
- Tag it **useful**, **maybe**, or **nothing**. Mark duplicates of an earlier idea as **dup (#n)**.
- Don't skip principles that look irrelevant. Ask briefly anyway.

Two modes:
- **Self-apply:** the assistant answers all 40 itself.
- **Prompt a human:** ask in batches of about 5, restating the contradiction each batch.

Record results in a table:

| # | Principle → question | Suggestion (proposal) | Tag |
|---|---|---|---|

## 3. Pick the top 3 to 5
Choose only ideas that would **actually change the design**, not polish. For each:
- **Why** it resolves the contradiction.
- **What it could make worse.**
- **Cheapest test** to confirm or rule it out (a calculation, sample run, prototype, or check on existing data).

## 4. Check against decisions already made
Compare every top idea to the decisions listed in step 1.
- If it matches something already decided, label it **rediscovery** (it confirms the decision; it isn't new).
- If it conflicts with a decision, say so plainly; don't quietly override it.
- Only ideas that are neither are **new**.

## 5. Report
- Tally: how many useful, maybe, nothing.
- The top ideas, each labeled new / rediscovery / conflict, with risk and test.
- What is still unproven.

## Rules
- Everything is a **proposal**. Nothing gets acted on from this output alone.
- A domain expert reviews the results before anyone acts.
- Don't invent data, specs, or numbers. Cite sources; mark the rest `ASSUMPTION`.
- Honest "nothing useful here" answers are a feature. Expect many on any single problem.

See [examples/data-normalization.md](examples/data-normalization.md) for a full worked run.
