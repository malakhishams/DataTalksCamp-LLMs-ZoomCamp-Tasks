# LLM Zoomcamp 2026 Module 4: Evaluation

This folder contains my homework solution for Module 4, which covers evaluating
a RAG pipeline: generating a synthetic ground-truth dataset, measuring retrieval
quality with Hit Rate and MRR, and comparing text, vector, and hybrid search.

## What I learned

- Generating a synthetic ground-truth dataset with an LLM (structured output)
- Hit Rate and MRR as retrieval evaluation metrics
- Comparing text search, vector search, and hybrid search (RRF) on the same
  ground truth
- Adapting structured-output parsing (Pydantic models) for Gemini, since its
  OpenAI-compatible endpoint doesn't support `response_format` the same way
  OpenAI's API does

## Setup

- LLM provider: **Google Gemini** (`gemini-2.5-flash`), via the OpenAI-compatible
  endpoint, `.env` file as in earlier modules
- Source data: lesson pages pulled from the course repo
  ([DataTalksClub/llm-zoomcamp](https://github.com/DataTalksClub/llm-zoomcamp),
  commit `8c1834d`) via the `gitsource` package
- Embeddings: local ONNX `all-MiniLM-L6-v2` model (`embedder.py`, from Module 2)
- Search: `minsearch` for text and vector search, `rrf` for hybrid

## Files

- `week4_task.ipynb` —> homework solutions
- `embedder.py` —> ONNX-based text embedder (from Module 2)
- `rag_helper.py` —> reusable RAG pipeline base class
- `evaluation_utils.py` —> Gemini structured-output helper, token/cost calculators
- `ground-truth.csv` —> synthetic Q&A ground truth generated from lesson pages

---

Part of the [LLM Zoomcamp 2026](https://github.com/DataTalksClub/llm-zoomcamp) by
[DataTalks.Club](https://datatalks.club/)
