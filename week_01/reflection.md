# Final Reflection

**1. Most useful thing I learned this week**
AI is a confident next-token predictor, not a source of truth. Because it writes fluent answers whether or not it is right, I have to verify anything that matters. I also learned that AI is software running on hardware (CPU, GPU, NPU, memory), so its speed and cost depend on the computing underneath.

**2. What I initially misunderstood**
I thought an AI model "looks up" answers or simply knows facts. In reality it predicts one token at a time from learned patterns, and it usually *samples* from probabilities instead of always picking the single most likely word. I also hadn't separated a chatbot from a tool-using assistant, RAG, and an agent. The difference is whether the system can retrieve information, use tools, and take steps toward a goal.

**3. What AI helped me do**
- Break down how LLMs work, first technically and then in beginner-friendly terms.
- Draft structured answers, tables, and diagrams for the missions.
- Think about where AI could help in DV, such as debugging failing regressions.

**4. Where I needed to verify or correct AI**
- The AI's one-sentence LLM summary said it predicts "the most likely next word." Sources showed it predicts *tokens* and samples instead of always taking the top one.
- In the UVM answer, the core idea matched my notes. But two details (where the cast happens, and what the `m_`/`p_` letters stand for) were unsupported by the source, even though they were stated just as confidently.

**5. One question for Saturday**
When AI is used for DV tasks like log debugging or generating UVM code, how do engineers check that its output is correct and keep company design data confidential at the same time?
