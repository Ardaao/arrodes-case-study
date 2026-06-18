# Lessons Learned

Building Arrodes was an exercise in managing the unpredictability of LLMs and turning that unpredictability into a reliable system.

## Key Technical Insights

### 1. The Reliability Gap
The biggest lesson was that **prompt engineering is not a substitute for system engineering**. While a good prompt can fix a problem 80% of the time, the remaining 20% requires structured guardrails, validation layers, and deterministic fallback mechanisms.

### 2. Memory is More Than a Vector Store
Initially, I relied solely on RAG. I quickly learned that semantic search is great for facts, but terrible for "state." Implementing a tiered memory system (Session $\rightarrow$ Project $\rightarrow$ Semantic) was the only way to maintain a consistent personality and goal-awareness over long periods.

### 3. The Importance of "The Loop"
Implementing a Reviewer agent changed the quality of the output significantly. The "Self-Correction" loop—where an agent's work is critiqued and sent back for iteration—is the most effective way to reduce hallucinations in complex tasks.

## Product & UX Lessons
* **The UI as a Debugger:** In agentic systems, the UI isn't just for the user; it's for the developer. Being able to see *why* an agent chose a specific tool is the only way to iterate effectively.
* **Proactivity vs. Intrusiveness:** Learning to balance "proactive notifications" was a challenge. The system is most useful when it alerts the user to a *meaningful* state change, rather than every minor detail.

## Final Reflections
This project demonstrated that the real value of AI today is not in the model itself, but in the **orchestration** around it. The ability to connect a reasoning engine to a set of reliable tools and a structured memory is what transforms a "chatbot" into a "system."
