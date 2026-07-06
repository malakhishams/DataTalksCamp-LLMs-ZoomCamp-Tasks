# LLM Zoomcamp 2026 Module 3: Orchestration

This folder contains my homework solution for Module 3, which covers orchestrating AI workflows with [Kestra](https://kestra.io/), including context engineering, RAG-grounded responses, and token usage in agentic flows.

## Setup

- Kestra run locally via Docker Compose (`docker compose up -d`), using the `docker-compose.yml` provided in the course's `03-orchestration` folder
- LLM provider: **Google Gemini** (`gemini-2.5-flash`), configured as a Kestra secret (`SECRET_GEMINI_API_KEY`)
- Flows used: `1_chat_without_rag.yaml`, `2_chat_with_rag.yaml`, `4_simple_agent.yaml` (all imported into the `zoomcamp` namespace)

## Files

- `week3_task.ipynb` : homework answers and reasoning
- `4_simple_agent_edited.yaml` : the `4_simple_agent` flow after editing the `english_brevity` task's prompt (Q5), changed from asking for exactly 1 sentence to exactly 3 sentences

## Course

Part of the [LLM Zoomcamp 2026](https://github.com/DataTalksClub/llm-zoomcamp) by [DataTalks.Club](https://datatalks.club/).