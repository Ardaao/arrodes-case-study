# Arrodes Case Study

Arrodes is a personal multi-agent AI assistant framework designed to bridge the gap between static LLM chat interfaces and a proactive, tool-capable personal operating system.

> **Note:** This is a public case study intended for portfolio and architectural review. The production source code remains private to protect sensitive implementation details and security configurations.

## What is Arrodes?
Arrodes is not just a wrapper around an LLM; it is a structured system designed to manage cognitive load, persist long-term memory, and interact with the physical and digital world through a set of specialized agents and integrated tools. It transforms the LLM from a chatbot into an autonomous coordinator capable of managing projects, monitoring systems, and executing complex workflows.

## Core Features
* **Multi-Agent Orchestration:** Separation of concerns between different agent roles (e.g., Researcher, Developer, Reviewer) to improve output quality.
* **Dynamic Tool Calling:** A flexible schema allowing the system to interact with external APIs, local files, and third-party services.
* **Hierarchical Memory:** A multi-layered approach combining short-term session history, semantic long-term memory, and project-specific context.
* **Proactive Workflows:** Scheduled "heartbeat" checks and automated notification systems that allow the assistant to initiate conversations based on state changes.
* **Omnichannel Interface:** Seamless interaction via a custom Web Dashboard and a Telegram gateway.

## Architecture Overview
The system follows a hub-and-spoke microservice approach, utilizing **Redis Streams** for asynchronous communication and **PostgreSQL** for robust state management. This ensures that the orchestration layer remains decoupled from the specific tool implementations.

## Tech Stack
* **Language:** Python
* **LLMs:** Multi-provider integration (OpenAI, DeepSeek, etc.)
* **Memory & Vector Store:** ChromaDB for semantic retrieval, PostgreSQL for session history.
* **Messaging & Coordination:** Redis Streams.
* **Gateways:** Telegram Bot API, WebSocket-based Web UI.

## Engineering Deep Dives
Detailed design decisions and implementation strategies can be found in the documentation:

* [Architecture Detail](./docs/architecture.md) — The high-level system design.
* [Tool Calling Strategy](./docs/tool-calling.md) — How Arrodes interacts with the world.
* [Memory & RAG Approach](./docs/memory-and-rag.md) — Semantic retrieval and memory bridges.
* [LLM Orchestration](./docs/llm-orchestration.md) — Agent roles and provider routing.
* [Deployment & Ops](./docs/deployment-and-ops.md) — Local-first constraints and observability.
* [Lessons Learned](./docs/lessons-learned.md) — Technical tradeoffs and insights.

## Visuals
*(Placeholders for architectural diagrams and UI screenshots)*
* **System Architecture:** `assets/diagrams/architecture_diagram.png`
* **Dashboard Preview:** `assets/screenshots/dashboard_main.png`
* **Telegram Interaction:** `assets/screenshots/telegram_flow.png`

## What I Learned
Building Arrodes provided deep insights into the challenges of LLM reliability, the necessity of structured memory to avoid context window exhaustion, and the importance of a robust tool-calling validation layer.

## Roadmap
* [ ] Enhanced multi-modal support (Vision/Audio).
* [ ] More granular agent permissioning.
* [ ] Automated evaluation pipeline for tool-calling accuracy.

---
*Developed as a personal exploration into the future of agentic workflows.*
