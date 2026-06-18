# Deployment & Operations

Arrodes was developed as a personal project with a "local-first" mindset, prioritizing data privacy and rapid iteration over cloud scalability.

## Local-First Constraints
Because the system manages personal data and interacts with local files, it is primarily deployed in a controlled environment. This approach avoids the complexity of cloud IAM and ensures that tool execution has direct access to the necessary local resources.

## Operational Components

### 1. Telegram Gateway
The Telegram bot serves as the primary remote interface. It allows me to interact with the system from anywhere without exposing a public API endpoint to the open web.

### 2. Web Dashboard
A custom dashboard provides a visual overview of the system's health, current agent activity, and a history of tool calls. This is essential for debugging the "black box" of LLM reasoning.

### 3. Heartbeat & Observability
To ensure the system is running, a **Heartbeat** mechanism is implemented:
* **Scheduled Checks:** The system periodically verifies the health of its internal services.
* **Proactive Alerts:** If a service fails or a critical error occurs, the system sends a notification via Telegram.

## Operational Lessons
* **Logging the "Thought Process":** I found that logging only the final output was insufficient. By logging the intermediate "thoughts" and tool-call attempts, I could identify exactly where a reasoning chain broke down.
* **State Recovery:** Using Redis Streams allowed the system to be resilient. If the core service restarted, it could recover the state of ongoing conversations without losing progress.
* **Environmental Isolation:** Using Docker for the database and Redis layers ensured that the system could be moved between different machines without worrying about dependency drift.
