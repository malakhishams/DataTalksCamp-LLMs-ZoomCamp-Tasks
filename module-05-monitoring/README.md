# Module 5: Monitoring

This module covers instrumenting a RAG system with [OpenTelemetry](https://opentelemetry.io/) (OTel) — capturing traces and spans, recording metrics as span attributes, persisting traces to SQLite, and analyzing trace data to understand system behavior (timing, cost, and stability).

This homework builds a lightweight, from-scratch tracing setup with the OTel SDK and a custom SQLite exporter.

## Setup

The RAG pipeline reuses the course-lessons knowledge base from Module 1 (72 lesson pages pulled from GitHub via `gitsource`, indexed with `minsearch`).

### Gemini adaptation

As in every prior module, the course code is written for OpenAI, so the LLM client and calls were adapted for Gemini's OpenAI-compatible endpoint:

- `client.chat.completions.create` instead of `client.responses.create`
- `"system"` role instead of `"developer"`
- `response.choices[0].message.content` instead of `response.output_text`
- `usage.prompt_tokens` / `usage.completion_tokens` instead of `usage.input_tokens` / `usage.output_tokens`

---

`rag_helper.py` and `starter.py` are otherwise unchanged from the provided starter package.

## Instrumentation

A `RAGTraced` subclass of `RAGBase` wraps `rag()`, `search()`, and `llm()`, each in its own OTel spa

Spans are persisted directly via a custom `SQLiteSpanExporter` that writes each finished span to a `spans` table in `traces.db`. Q1-Q3 are answered by querying the first trace's rows rather than inspecting console output.

### Notes

- The `rag` span wraps both `search` and `llm`, so it was excluded from the Q5 time comparison to avoid double-counting.
- `search` (in-memory minsearch lookup) consistently took under 10-20ms, while `llm` (the Gemini API call) took 2-6+ seconds — the LLM call dominates total request time by roughly 900x.
- Across 7 runs, input token counts were highly stable (7933-8238), confirming the retrieval step returns consistent context for the same query.

## Files

- `starter.py` — loads the course lessons, builds the minsearch index, wraps it in `RAGBase` (Gemini client configured here)
- `rag_helper.py` — `RAGBase` class (search, prompt building, Gemini LLM call)
- `homework5.ipynb` — notebook with the `RAGTraced` instrumentation, console/SQLite exporter setup, and analysis for Q1-Q6
