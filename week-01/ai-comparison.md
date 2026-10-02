# Week 01 AI Assistant Comparison

## Common question
`is sv event and verilog event same`

## Tool 1
Name: Claude
Answer summary: SV keeps Verilog's event model and extends it (`.triggered`, `->>`, event aliasing, `null`, more scheduler regions, clocking blocks).
Strengths: Broad, well organized, correct core point.
Weaknesses: Region list presented as complete, "may hang" understated, unsupported mailbox/semaphore claim.

## Tool 2
Name: ChatGPT
Answer summary: Same basic mechanism; SV adds `event.triggered()` to avoid missed events.
Strengths: Concise, practical, correct core point.
Weaknesses: Wrote `triggered()` as a method, contradicted by its own code. Narrower coverage.

## Verification source
IEEE 1800-2017 LRM, Chapters 4 and 15, plus a simulator run.

## Final comparison
- Accuracy: Both correct on the main idea; each had minor errors.
- Traceability: Neither gave sources unprompted.
- Explanation quality: Claude broader, ChatGPT more concise.
- Ease of verification: Syntax and code claims were easy to test; completeness claims needed the LRM.
- Claims needing correction: `triggered()` syntax, the region list, "may hang".

## Lesson
Both assistants were useful for explanation but not authoritative. Check details like syntax and completeness against the standard.
