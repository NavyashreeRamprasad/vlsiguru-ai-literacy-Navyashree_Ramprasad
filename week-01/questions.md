# Week 01 Questions
## Q1 - AI → ML → Deep Learning → Generative AI → Agents
### A - Answer - 
- AI is the big umbrella. It's any computer system that does things we would normally say need human thinking, like understanding language, spotting patterns, or making decisions.
- Machine learning is one way of doing AI. Instead of writing every rule by hand, you show the computer lots of data and it finds the patterns itself.
- Deep learning is a type of machine learning that uses neural networks with many layers. The deep just means lots of layers.
- Generative AI is AI that creates new things like text, images, audio or code, instead of only recognizing or predicting.
- AI agent is a whole system, not just a model. It's a model plus tools plus a loop, so it can decide what to do next, act, check the result, and keep going.
  
```mermaid
flowchart TD
    AI["Artificial intelligence"] --> ML["Machine learning"]
    ML --> DL["Deep learning"]
    DL --> GEN["Generative AI"]
    AGENT["AI agent: model + tools + loop"] -.->|calls a model| GEN
```
Examples:
- AI: Google Maps working out the fastest route home
- Machine learning:	Gmail's spam filter getting better as you mark emails as spam
- Deep learning: Your phone unlocking when it recognizes your face
- Generative AI	: Asking a chatbot to write a leave application for you
- AI agent:	A travel assistant that searches flights, checks your calendar, compares prices, and books the best one, adjusting if something fails
### E - Evidence - 
- https://www.ibm.com/think/topics/ai-vs-machine-learning-vs-deep-learning-vs-neural-networks
- https://docs.cloud.google.com/distributed-cloud/hosted/docs/latest/gdcag/application/ao-user/genai/genai-overview
- https://www.anthropic.com/engineering/building-effective-agents
### V - Verification - 
- IBM says ML is a subset of AI and DL is a subset of ML. It also says a network needs more than three layers to count as deep learning.
- Google Cloud says generative AI creates new content with characteristics similar to its training data.
- Anthropic says agents are systems where the model directs its own process and tool use.
All three matched my explanations.
### R - Reflection - 
The first four terms are easy to line up because each is a smaller part of the one before it. Agents were the odd one out because they describe how a system is built, not a kind of model.

  
## Q2 - Is Everything That Looks Intelligent Actually AI?
### A - Answer 
- Traditional software (not AI)
    - Calculator: 25 × 16 = 400 : It follows fixed arithmetic rules and gives the same answer every time. Nothing is learned.
    - If temperature > 80°C, display WARNING : A human wrote the rule and the threshold. The program only checks it.
- Machine learning based AI
    - Email system flags spam from patterns learned from past emails : It learned patterns from old email data instead of someone writing a rule for every kind of spam.
    - Navigation app predicts arrival time from traffic and historical data : It predicts a number using patterns found in historical data.
- Generative AI
    - AI assistant writes a summary of a document : It creates new text, not just a label or a number.
### E - Evidence - https://docs.cloud.google.com/distributed-cloud/hosted/docs/latest/gdcag/application/ao-user/genai/genai-overview
### V - Verification -For each scenario I asked two questions: did a human write the rule, or did the system learn it from data? And does it create new content?
- A and B have no learning step, so they're not AI.
- C and E learn from data and output a label or a number, so they're ML.
- D creates new text, so it's generative AI.
- I classified E from the description in the question. I didn't check how any real navigation app is actually built.
### R - Reflection - 
Real products often mix both. A spam filter can have hand-written rules and a learned model together, so I classified by the main behavior. Looking smart isn't enough to call something AI. The real test is whether the behavior comes from learning or from fixed rules.

## Q3 - What Happens When You Ask an LLM a Question?
### A - Answer 
```mermaid
flowchart TD
    P["Prompt<br/>Your text goes in"] --> T["Tokens<br/>Text cut into pieces, turned into numbers"]
    T --> M["Model processing<br/>Reads all tokens in the context together"]
    M --> D["Probability distribution<br/>A probability for every possible next token"]
    D --> S["Next token selection<br/>Pick one: most likely, or sampled"]
    S --> R["Generated response"]
    S -.->|"add token to context, then predict again"| M
```
- Prompt: the text you send to the model, like "What is the capital of France?"
- Tokens: the model can't read words the way we do. Your text is cut into small pieces called tokens (a word or part of a word), and each piece is turned into a number.
- Model processing: the model looks at all the tokens in its context, meaning your prompt plus anything it has already written, and works out which tokens are likely to come next.
- Probability distribution: the model gives every possible next token a probability. "Paris" might get a very high one and unrelated words get tiny ones.
- Next token selection: one token is picked, either the most likely one or one sampled from the likely ones. This is next-token prediction.
- Generated response: the chosen token is added to the context and the model predicts again. This repeats until the answer is finished, and the full text is the response.
### E - Evidence - https://developers.google.com/machine-learning/crash-course/llm
### V - Verification -I matched each stage in my diagram against both sources. Tokens, probabilities, and picking the next token all appear in them.
- The "repeat the loop" step matches the slides' description of generating text from the text generated so far.
- The point that nothing in the loop looks up facts is my own reasoning from how the loop works, not a quote from either source.

### R - Reflection - 
Sampling explains why the same prompt can give different answers on different tries. It also means a fluent answer needs checking like any other claim, which is why verification matters. One thing I'm still unsure about is how the model "reads all tokens together" in step 3. That's the attention idea, which I'll learn in a later week.


## Q3 - Hallucination Experiment: Can AI Sound Confident and Still Be Wrong?
### A - Answer 
# Hallucination Experiment: Can AI Sound Confident and Still Be Wrong?

## Experiment table

| Field | Entry |
|---|---|
| **Prompt (exact wording)** | `is sv event and verilog event same` |
| **Model A** | Claude |
| **Model A response summary** | Says SystemVerilog keeps Verilog's event model and extends it. Lists `.triggered`, `->>`, event assignment/aliasing, `null` events, extra scheduling regions, clocking blocks, and more. |
| **Model B** | ChatGPT |
| **Model B response summary** | Says the basic `event`, `->`, `@` mechanism is the same and SV adds `event.triggered()` to avoid missed events. Includes an "interview answer". |

### Claims checked

| # | Claim | Source of claim | Evidence (IEEE 1800, verify section) | Result |
|---|---|---|---|---|
| 1 | `@e` can miss an event triggered earlier; `wait(e.triggered)` avoids this because the triggered state persists for the time slot | Claude and ChatGPT | §15.5.3 (`triggered` property) | **Correct** |
| 2 | `triggered` is written as a method: `event.triggered()` | ChatGPT | `triggered` is a property accessed as `e.triggered`, with no call parentheses. ChatGPT's own code uses `done.triggered`, so it contradicts itself. | **Wrong / self-contradictory** |
| 3 | Scheduler regions are Preponed, Active, Inactive, NBA, Observed, Reactive, Re-Inactive, Re-NBA, Postponed | Claude | §4 defines more regions (Pre-Active, Pre-NBA, Post-NBA, Pre-Observed, etc.). | **Incomplete**, presented as complete |
| 4 | `-> e; @(e);` in the same process "may hang" | Claude | If the trigger comes first in the same process, the wait never sees it, so it will hang unless re-triggered. | **Imprecise** (understated) |
| 5 | Mailboxes and semaphores "build on event-style synchronization" | Claude | No supporting wording found in the LRM. | **Unsupported / loosely worded** |
| 6 | SV events can be aliased (`e1 = e2`), passed to tasks, and set to `null` | Claude | §15.5.1 and §15.5.2 | **Correct** |
| 7 | Verilog and SV share the same `event` / `->` / `@` basics | Claude and ChatGPT | §15.5 | **Correct** |

## Result

Both answers were correct on the main idea (same basic mechanism, SV adds `.triggered` for race avoidance). Each had a flaw:

- **ChatGPT:** syntax error (`triggered()`), contradicted by its own example.
- **Claude:** simplified or loosely worded details (region list, mailbox/semaphore claim, "may hang").

The test did not expose a major failure because the question was broad and the core answer is well documented. A narrower question (for example, exact region ordering or `->>` behavior) would be more likely to expose errors.

## Lesson

A correct overall answer can hide small technical errors. Both errors were stated in the same confident tone as the correct claims. In HDL work, wrong syntax or a list presented as complete can cost real debug time, so verify specific claims against the standard.

## Reflection

An AI answer can sound convincing because language models generate text that is statistically plausible, not text checked against a source. Clear structure, confident headings, tidy code examples, and even an "interview answer" make the output feel authoritative whether or not the facts are solid. Correct and incorrect details come in the same tone, so confidence in the wording says nothing about accuracy. Agreement between two agents is also weak evidence, since they may share the same training-data biases. Verification means checking the claims that matter (syntax, definitions, edge cases) against a primary source such as the IEEE 1800 LRM.
