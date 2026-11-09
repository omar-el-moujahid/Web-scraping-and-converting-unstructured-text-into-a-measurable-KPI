# Scraping to KPI

A small local pipeline that turns job posting text into one published KPI: the share of postings mentioning a chosen skill.

## Pipeline

1. `scripts/extract_skills.py` uses a local Ollama model to extract skills from each posting.
2. `scripts/compute_kpi.py` aggregates those skills into `docs/data/kpi.json`.
3. `docs/index.html` displays the KPI and the most-mentioned skills on GitHub Pages.

## Run

Requires Python, Ollama, and a local `data/jobs_sample.csv` file with `title`, `company` and `description` columns.

```bash
pip install requests
ollama pull qwen3:8b
python scripts/extract_skills.py 15
python scripts/compute_kpi.py
cd docs
python -m http.server 8000
```

Then open http://localhost:8000.

## Data

`data/jobs_sample.csv` and `data/extracted.json` stay local and are ignored by Git. Only the aggregate file `docs/data/kpi.json` is published.

## Limits

The sample is small, and LLM extraction can vary between runs or miss and invent skills. Treat the KPI as an indication, not as proof of market demand.