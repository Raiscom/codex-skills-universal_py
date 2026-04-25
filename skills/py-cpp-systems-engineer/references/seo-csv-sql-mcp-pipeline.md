# SEO CSV to SQL to MCP Analytics Pipeline

Use this reference when the task is to build a production Python system that ingests SEO and analytics CSV report sets into SQL and exposes bounded AI access through MCP-style tools.

## Goal

Build an architecture where raw CSV files are sources, SQL tables/views are the analytical surface, and AI works through schemas, samples, summaries, and safe read-only queries instead of reading large CSV files directly.

## Default Assumptions

- local database: DuckDB;
- PostgreSQL only when multi-user or service deployment requires it;
- Python 3.11+;
- large imports are batched;
- MCP-side access is read-only and bounded.

## Report Sources

Support CSV reports such as:

- Yandex Metrica;
- behavioral metrics;
- semantic/keyword reports;
- technical SEO audits;
- competitor reports;
- other SEO exports.

## Architecture

Use layered modules:

- `config/`
- `ingestion/`
- `loaders/`
- `schema/`
- `transform/`
- `storage/`
- `mcp_server/`
- `queries/`
- `models/`
- `tests/`

Data flow:

```text
CSV folder -> detection -> raw tables -> staging tables -> marts/views -> MCP tools
```

## Ingestion

The system should:

- scan a folder of CSV files;
- detect report type by filename, header pattern, and schema;
- validate required columns;
- normalize data types;
- handle Russian and English headers;
- handle delimiters, encodings, empty values, dates, floats, and schema drift;
- log skipped rows/files;
- support repeatable loads without duplicates.

## Storage Layers

Prefer:

- `raw_*` tables for imported source data;
- `stg_*` tables for normalized staging data;
- `mart_*` views or tables for analytical aggregates.

Common entities:

- dates;
- visits/sessions;
- landing pages;
- exit pages;
- traffic sources;
- search queries;
- behavioral metrics;
- technical issues;
- competitors;
- rankings/SERP data;
- domains, pages, regions, and devices.

## Analytical Views

Prepare views for:

- traffic trends;
- top landing pages;
- top exit pages;
- traffic sources;
- keyword and semantic analysis;
- behavioral metrics;
- technical issue summaries;
- period-over-period comparison;
- page + traffic + behavior + semantic linkage;
- competitor + keyword + position linkage.

## MCP Tool Surface

Expose safe tools such as:

- `list_tables`
- `describe_table`
- `preview_table`
- `run_safe_query`
- `get_kpi_summary`
- `compare_periods`
- `top_landing_pages`
- `top_exit_pages`
- `keyword_competitor_overlap`
- `technical_issues_summary`

SQL access must be read-only, checked against unsafe statements, result-limited, and logged.

## Default Stack

- `pydantic`
- `loguru`
- `tenacity`
- `duckdb`
- `pandas` or `polars`
- `pyarrow` when useful
- `typer`
- `pytest`
- `ruff`

For PostgreSQL support, add `sqlalchemy` and `psycopg`.

## Tests

Cover:

- CSV report type detection;
- column normalization;
- database loading;
- de-duplication or upsert behavior;
- safe SQL restrictions;
- at least one MCP-facing tool.
