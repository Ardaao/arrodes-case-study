# Architecture Overview

Arrodes is designed as a decoupled system where the intelligence (LLM) is separated from the execution (Tools) and the state (Memory). This ensures that the system can scale in capability without becoming a monolithic, fragile script.

## System Components

### 1. Interfaces (The Gateways)
Arrodes interacts with the user through two primary channels:
* **Web Dashboard:** A WebSocket-based interface for real-time interaction and system monitoring.
* **Telegram Gateway:** A lightweight bridge allowing the assistant to be accessible on the go and enabling proactive notifications.

### 2. Orchestration Layer
The core of the system acts as the "brain," managing the flow of information. It handles:
* **Request Routing:** Determining which agent or tool is best suited for a task.
* **State Management:** Tracking the current phase of a multi-step conversation.
* **Context Assembly:** Gathering relevant data from the memory layer before sending a prompt to the LLM.

### 3. Tool Layer
Instead of hard-coding functions, Arrodes uses a structured tool-calling mechanism. Each tool is defined by a schema that the LLM understands. This allows for:
* **Extensibility:** New tools can be added without modifying the core orchestration logic.
* **Isolation:** Tools are executed in a controlled environment, ensuring that a failure in one tool doesn't crash the entire system.

### 4. Memory & Context Layer
To overcome the limitations of context windows, Arrodes implements a tiered memory system:
* **Short-term:** Recent messages stored in PostgreSQL.
* **Semantic:** Embeddings stored in ChromaDB for "fuzzy" retrieval of past experiences.
* **Project-specific:** Dedicated context buckets for specific long-term goals.

### 5. Persistence & Messaging
* **Redis Streams:** Used as the backbone for asynchronous communication between the core and the gateways.
* **PostgreSQL:** The source of truth for user data, session history, and system configurations.

## Proactive Workflows
Unlike traditional chatbots, Arrodes includes a **Scheduler** that performs periodic "heartbeat" checks. If the system detects a state change (e.g., a deadline approaching or a system alert), it can trigger a proactive notification via Telegram, shifting the assistant from a reactive tool to a proactive partner.

---
*Private Implementation Note: The actual source code utilizes a modular service structure to ensure that gateways and core logic can be developed and deployed independently.*
