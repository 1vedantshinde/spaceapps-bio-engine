# Space Biology Knowledge Engine
# SpaceApps AI Summarization Pipeline

This workspace ingests NASA space biology publications and produces structured metadata, knowledge-graph triples, semantic-search indices, and multi-level summaries ready for an AI summarization dashboard.

## Directory Highlights

- `scripts/`: end-to-end automation (ingest, parsing, normalization, KG, embeddings, summaries).
- `data_raw/`: original CSV + manifest (and optional HTML/PDF snapshots).
- `data_parsed/`:
  * `metadata_master.jsonl`, `sections/`, `relations/candidates.jsonl`
  * `embeddings/` (FAISS index, chunk metadata, embeddings, meta)
  * `summaries/` (snippets, section summaries, paper bullets, topic reports)
- `kg/`: graph triples (`graph.csv`, `graph.ttl`)
- `db/papers.sqlite`: normalized metadata table.
- `.gitignore`: excludes large regenerable artifacts (`data_raw/html/`, `data_raw/pdfs/`, `embeddings.npy`, `faiss.index`, `.venv/`).

## Environment Setup

