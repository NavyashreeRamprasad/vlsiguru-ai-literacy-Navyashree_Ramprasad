# Week 01 Verification Log

| Date | Question / claim | AI tool | Claim checked | Verification source / experiment | Result |
|---|---|---|---|---|---|
| 29/9/26 | Q4 | Claude, ChatGPT | `@e` can miss an earlier trigger; `wait(e.triggered)` avoids it | IEEE 1800-2017 §15.5 (event section)| Correct |
| 29/9/26| Q4 | ChatGPT | `triggered` is written as a method: `event.triggered()` | IEEE 1800-2017 §15.5.3. `triggered` is a property accessed as `e.triggered`. ChatGPT's own code used `done.triggered`. | Wrong, and self-contradictory |
| 29/9/26| Q4 | Claude | Scheduler regions listed as complete | IEEE 1800-2017 Chapter 4. Standard lists more regions (e.g. Pre-Active, Pre-NBA, Post-NBA). | Incomplete |
| 29/9/26| Q4 | Claude | `-> e; @(e);` in one process "may hang" | EDA Playground run of the two-line example  | Understated: it does not wake|
| 29/9/26| Q4 | Claude | Events can be aliased, passed to tasks, set to `null` | IEEE 1800-2017 §15.5.5 (event operations) | Correct |
| 29/9/26 | Q4 | Claude | Mailboxes and semaphores "build on" events | Searched the LRM for supporting wording | Unsupported |
| 29/9/26| Q5 | Claude | HTTP 404 means "Not Found" and is defined in RFC 9110 | RFC 9110 §15.5.5 and IANA status code registry, opened directly | Correct but incomplete: missed "or unwilling to disclose existence" |
|  30/9/26 | Q8 | None (web sources) | Gmail, Maps, Netflix, Face ID use ML | Original Google, DeepMind, Netflix, Apple pages  |  Sources are dated (2015 to 2020) |
|  30 /9/26 | Q8 | None | Traffic signal AI involvement | No public evidence found | Not enough public evidence to conclude |
|  2/9/26 | Q10 | Claude | EMI on ₹5,00,000 at 10% for 5 years is about ₹10,624 | Spreadsheet `=PMT(10%/12, 60, -500000)` | Expected ₹10,623.5, rounds to ₹10,624 |

## Notes

**What did the AI get right?**
Both assistants got the core SystemVerilog event idea right and explained the missed-event race clearly. The 404 answer was also correct.

**What did it get wrong or leave unsupported?**
ChatGPT wrote `triggered()` as a method. Claude presented an incomplete region list as complete and made an unsupported mailbox/semaphore claim. The 404 answer left out part of the RFC wording.

**What did I learn about verification?**
Confident tone did not predict accuracy. Syntax, completeness, and wording like "may" needed a primary source or a test. Reposts of sources are not the same as opening the original.

