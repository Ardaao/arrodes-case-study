# Memory & RAG Approach

The primary constraint of any LLM-powered system is the "context window." Arrodes solves this by implementing a hierarchical memory system that mimics human cognitive layers.

## Memory Layers

### 1. Short-Term Session History
The most recent messages are stored in a relational database (PostgreSQL). This provides the LLM with the immediate context of the current conversation, ensuring fluid and coherent dialogue.

### 2. Semantic Memory (Long-Term)
For information that isn't immediately relevant but might be needed later, Arrodes uses **RAG (Retrieval-Augmented Generation)**:
* **Embedding:** Text is converted into high-dimensional vectors.
* **Storage:** These vectors are stored in **ChromaDB**.
* **Retrieval:** When a user asks a question, the system performs a semantic search to find the most similar past experiences or documents and injects them into the prompt.

### 3. Project Memory
Certain tasks require a stable, long-term set of constraints and goals. Project memory acts as a "pinned" context that the LLM always references when working on a specific project, preventing the "forgetting" that occurs in long sessions.

### 4. The Memory Bridge (Summarization)
To prevent the short-term history from overflowing the context window, Arrodes uses a **summarization bridge**. When a conversation reaches a certain length, the system summarizes the key points and "archives" them into the semantic memory, maintaining a condensed version of the history in the active window.

## Tradeoffs and Failure Modes
* **Retrieval Noise:** Sometimes the RAG system retrieves "similar" but irrelevant information. I mitigated this by refining the embedding models and implementing a relevance threshold.
* **Latency:** Performing vector searches adds a small overhead. This was managed by optimizing the retrieval pipeline and using asynchronous processing.
* **Consistency:** Updating a memory that was previously stored can be tricky. Implementing a "read-update-write" cycle for semantic memory was key to maintaining accuracy.
