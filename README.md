# TRIZ 40 Questions Skill

A structured problem-solving skill for AI assistants (or people) based on TRIZ's 40 inventive principles. Use it when you're stuck on a design, product, or process problem, or going in circles.

It makes the assistant:
1. State the problem and its core contradiction.
2. Ask all 40 principles as questions, in order, giving a concrete idea or an honest "nothing useful here" for each.
3. Tag every result useful / maybe / nothing.
4. Pick the top 3 to 5 ideas that would actually change the design, with what each could make worse and the cheapest test for it.
5. Check the ideas against decisions already made, labeling rediscoveries as such.
6. Present everything as proposals for a domain expert to review.

## Files
- `SKILL.md` — the procedure (with front matter for assistants that load skills).
- `questions.md` — all 40 principles: name, question, plain explanation.
- `examples/data-normalization.md` — a worked run on a real-world style problem.

## How to use
- **Skill-aware assistants** (agents that load `SKILL.md` files): copy this folder into your skills directory.
- **Any chat assistant:** paste `SKILL.md` and `questions.md` into the conversation, then describe your problem and the decisions you've already made. Ask it to "run the TRIZ 40 questions skill."
- **By hand:** work through `questions.md` yourself or with a team, in batches of about 5.

Expect around half the principles to produce nothing for any one problem. That's normal. The value is in the few ideas you wouldn't have reached otherwise, and in the honest filtering.
