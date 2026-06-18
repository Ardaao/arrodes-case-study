# LLM Orchestration

Arrodes is designed to be model-agnostic. It treats the LLM as a reasoning engine that can be swapped or routed based on the complexity of the task.

## Multi-Provider Approach
Different LLMs have different strengths. Arrodes supports multiple providers (OpenAI, DeepSeek, etc.), allowing for:
* **Cost Optimization:** Routing simple tasks to smaller, cheaper models.
* **Quality Boosting:** Using high-reasoning models (like GPT-4 or DeepSeek-Coder) for complex architecture or debugging tasks.
* **Redundancy:** Switching providers if one service experiences an outage.

## Agent Roles & Separation
To reduce "hallucinations" and increase precision, Arrodes utilizes a multi-agent pattern. Instead of one giant prompt, tasks are divided among specialized roles:
* **The Researcher:** Focuses on gathering data and exploring the RAG memory.
* **The Developer:** Focuses on writing code and utilizing system tools.
* **The Reviewer:** Critiques the output of other agents, ensuring it meets the project's quality standards.

This "adversarial" or "collaborative" loop ensures that a final answer is vetted before being presented to the user.

## Routing by Task Type
The orchestration layer analyzes the user's intent to determine the routing strategy:
* **Direct Response:** For simple queries $\rightarrow$ Simple LLM call.
* **Tool-Based Task:** For actions $\rightarrow$ Agent $\rightarrow$ Tool $\rightarrow$ LLM interpretation.
* **Complex Research:** For deep dives $\rightarrow$ Researcher Agent $\rightarrow$ RAG $\rightarrow$ Reviewer Agent $\rightarrow$ Final Response.

## Implementation Tradeoffs
The main tradeoff is **latency**. Every time a request passes through a "Reviewer" or multiple agents, the time-to-first-token increases. I balanced this by implementing a "Fast Path" for simple queries and a "Deep Path" for complex tasks.
