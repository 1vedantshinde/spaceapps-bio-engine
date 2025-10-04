
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
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt # generate with: pip freeze > requirements.txt


## Pipeline
python scripts/fetch_publications.py
python scripts/extract_sections.py
python scripts/normalize_metadata.py
python scripts/extract_relations.py
python scripts/build_kg.py
python scripts/build_embeddings.py
python scripts/summarize_snippets.py
python scripts/summarize_sections.py
python scripts/summarize_paper.py
python scripts/summarize_topic.py "bone loss microgravity"


Re-run downstream steps after new ingests.

## Dashboard Data Sources

- Listings/filters: `data_parsed/metadata_master.jsonl` or `db/papers.sqlite`
- Detailed text: `data_parsed/sections/*.json`
- Knowledge graph: `data_parsed/relations/candidates.jsonl`, `kg/graph.csv`, `kg/graph.ttl`
- Semantic search: `data_parsed/embeddings/`
- Summaries: files in `data_parsed/summaries/`

## Notes on Large Files

`data_raw/html/`, `data_raw/pdfs/`, `data_parsed/embeddings/embeddings.npy`, `faiss.index` are excluded in `.gitignore`. Regenerate them locally or store via Git LFS/shared storage if needed.

regenerate gitignore if not already done
