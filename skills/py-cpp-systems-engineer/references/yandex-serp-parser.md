# Yandex SERP Competitor Keyword Research

Use this reference when the task is to build a production Python project that determines which search queries selected competitor domains rank for in Yandex.

## Goal

Build a maintainable system that accepts competitor domains, region, device type, SERP depth, and keyword sources; fetches SERP data; detects competitor positions; persists results; and exports reports.

## Inputs

- competitor domains;
- Yandex region;
- device type: `desktop` or `mobile`;
- SERP depth: top 10, top 20, top 50, or similar;
- keyword sources:
  - CSV file;
  - suggestions;
  - sitemap/category/title/H1 extraction from competitor sites;
  - merged mode.

## Outputs

- `keywords`
- `competitors`
- `serp_checks`
- `serp_results`
- `competitor_hits`
- per-domain reports with keyword, position, ranking URL, appearance count, average position, and top-N counts
- CSV plus SQLite or DuckDB export for downstream analysis

## Default Stack

- Python 3.11+
- `httpx`
- `pydantic`
- `tenacity`
- `loguru`
- `typer` or `argparse`
- `pytest`
- `ruff`
- DuckDB or SQLite

## Architecture

Split modules by responsibility:

- `config/`
- `clients/`
- `providers/`
- `parsers/`
- `services/`
- `storage/`
- `models/`
- `tests/`

Keep these concerns separate:

- keyword acquisition;
- SERP retrieval;
- domain and URL normalization;
- ranking and position logic;
- persistence;
- reporting and export.

## Required Abstractions

Create a `SERPProvider` interface with backends such as:

- API provider;
- XML provider;
- HTML parser fallback;
- mock provider for tests.

Create a `KeywordSource` interface with sources such as:

- CSV source;
- sitemap/category crawler source;
- suggestion source;
- merged source.

## Domain Normalization

Handle:

- `www` vs non-`www`;
- `http` vs `https`;
- subdomains;
- root-domain comparison and exact-host comparison;
- URL normalization before persistence.

## Fault Tolerance

Include:

- timeouts;
- retries with backoff;
- bounded concurrency for large jobs;
- rate limiting;
- checkpointing;
- partial resume;
- intermediate persistence.

## Pipeline

1. Load configuration.
2. Collect keywords.
3. Clean, deduplicate, and normalize keywords.
4. Fetch SERP data in batches.
5. Parse result pages.
6. Detect target competitor domains.
7. Persist raw and normalized results.
8. Build aggregate reports.
9. Export CSV and SQL-ready data.

## Real Risks

- anti-bot protection;
- unstable HTML layouts;
- regional SERP differences;
- device-specific ranking differences;
- low-quality or biased keyword sources.
