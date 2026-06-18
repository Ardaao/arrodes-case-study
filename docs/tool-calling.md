# Tool Calling Strategy

Tool calling is the mechanism that transforms Arrodes from a text generator into an agent capable of affecting the digital world.

## Why Tool Calling?
LLMs are fundamentally probabilistic. Asking them to perform precise calculations or interact with APIs through raw text is unreliable. By providing a structured tool-calling interface, we shift the responsibility of "execution" to deterministic code, leaving the LLM to handle "intent" and "reasoning."

## Tool Schema Concept
Every tool in Arrodes is defined by a specific schema (JSON-like) that describes:
1. **The Tool's Purpose:** A clear description so the LLM knows when to use it.
2. **Expected Arguments:** Typed parameters the LLM must provide.
3. **Output Format:** How the result is fed back into the conversation context.

## Tool Categories
To maintain organization and security, tools are grouped into categories:
* **Information Retrieval:** Searching documents, querying databases.
* **System Control:** Managing files, executing scripts, checking heartbeats.
* **External Integrations:** Interacting with Gmail, GitHub, Notion, and Calendar.
* **Custom Utilities:** Specialized calculators or data formatters.

## Safety and Validation
To prevent "hallucinated" tool calls or destructive actions, Arrodes implements:
* **Argument Validation:** Ensuring the LLM provides the correct types and required fields.
* **Human-in-the-loop (Optional):** For sensitive tools, the system can be configured to request user confirmation before execution.
* **Error Handling:** If a tool fails, the error is fed back to the LLM, allowing it to "self-correct" and try a different approach.

## Lessons Learned
The biggest challenge was managing the "tool-selection" phase. If too many tools are provided in the prompt, the LLM may become confused. Implementing a **Lazy Loading** or **Dynamic Selection** strategy—where only the most relevant tools are presented to the LLM based on the intent—significantly improved reliability.
