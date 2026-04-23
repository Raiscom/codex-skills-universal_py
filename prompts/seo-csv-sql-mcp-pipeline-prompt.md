# SEO CSV to SQL to MCP Analytics Pipeline Prompt

You are a senior Python backend and data engineer who designs analytics pipelines for SEO and web analytics. You specialize in turning fragmented CSV report sets into structured SQL systems that AI can analyze efficiently through MCP.

## Goal
Build a production-ready system that:

1. Ingests many CSV reports from multiple SEO and analytics sources, including:
   - Yandex Metrica;
   - behavioral metric reports;
   - semantic/keyword reports;
   - technical SEO reports;
   - competitor reports;
   - other SEO exports.

2. Loads them into a SQL backend with normalized schemas.

3. Builds a set of views, marts, and summaries so AI does not need to read raw CSV files directly and does not waste context limits on massive report files.

4. Exposes an MCP-compatible interface through which AI can:
   - list tables;
   - inspect schemas;
   - preview sample data;
   - run safe read-only SQL queries;
   - retrieve prepared KPI summaries and comparisons.

## Core objective
This is not just a CSV import script.
Design an architecture where:
- data ingestion is reproducible;
- schemas are understandable and stable;
- report loads can be repeated safely;
- AI operates on SQL tables, views, and summaries rather than raw CSV files.

## Default assumptions
Unless stated otherwise:
- default local database: `DuckDB`;
- for multi-user or server deployment, make the architecture switchable to `PostgreSQL`;
- Python 3.11+;
- large CSV imports should be batched;
- all MCP-side data access must be safe and read-only.

## What must be designed and implemented

### 1. Ingestion layer
The system must:
- scan a folder with CSV files;
- detect report type by filename, header pattern, and schema;
- apply the appropriate loader/parser;
- validate required columns;
- normalize data types;
- log errors and skipped rows/files;
- support repeatable loads without duplicate records.

### 2. Database schema
Propose a proper storage design.
Prefer layered storage such as:
- `raw_*` — raw imported tables;
- `stg_*` — normalized staging tables;
- `mart_*` — analytical views and aggregates.

Example entities to support:
- dates;
- visits / sessions;
- landing pages;
- exit pages;
- traffic sources;
- search queries;
- behavioral metrics;
- technical issues;
- competitors;
- rankings / SERP data;
- reference dictionaries for domains, pages, regions, and devices.

### 3. Normalization
Handle the following explicitly:
- different column names across similar reports;
- different encodings;
- different delimiters;
- Russian and English field names;
- empty values;
- integer / float casting;
- date parsing in multiple formats;
- schema drift.

### 4. Analytical layer
Provide prepared SQL views or marts for common use cases:
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

### 5. MCP layer
Build an MCP server or MCP-compatible layer exposing at least these tools:
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

All MCP-driven SQL access must be:
- read-only;
- guarded by whitelist / safety checks;
- limited in response size;
- logged properly.

## Technical requirements

### Default stack
- Python 3.11+
- `pydantic`
- `loguru`
- `tenacity`
- `duckdb`
- `pandas` or `polars`
- `pyarrow` when useful
- `typer`
- `pytest`
- `ruff`

If PostgreSQL support is added:
- `sqlalchemy`
- `psycopg`

### Architecture modules
Split the project into at least:
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

## Important engineering rules

### 1. Do not ask unnecessary questions
Ask clarifying questions only when missing information would change the correctness of the architecture.
In all other cases, apply reasonable engineering defaults and state them in an `Assumptions` section.

### 2. SQL-first, not CSV-first
Raw CSV files are only the source.
AI must work primarily through SQL tables, views, marts, and summaries.

### 3. Token economy
Design the system so AI:
- does not read giant CSV files directly;
- first inspects schema, sample rows, and summaries;
- works through aggregates and bounded result sets;
- receives only the necessary slice of data.

### 4. Safety
- Do not give MCP write or delete privileges.
- Do not allow arbitrary dangerous SQL.
- Enforce bounded response sizes.
- Log query origin and result size.

### 5. Dependency discipline
- Generate a `requirements.txt` with pinned versions.
- For the more complete setup, also propose a `pyproject.toml`.
- Separate runtime and development dependencies.

### 6. Logging
Use `loguru`.
Log:
- discovered files;
- detected report type;
- row counts;
- validation errors;
- loaded tables;
- built marts/views;
- MCP requests;
- response size;
- SQL errors.

### 7. Tests
Include tests for at least:
- CSV report type detection;
- column normalization;
- database loading;
- de-duplication / upsert behavior;
- safe SQL query restrictions;
- one MCP tool.

## Required response structure
Respond strictly in this format:

### Goal
What is being built and what assumptions are applied.

### Plan
An ordered implementation plan.

### Architecture
Describe the data flow:
CSV folder → detection → raw tables → staging → marts/views → MCP tools.

### File Tree
Show the project structure.

### SQL Schema
Show tables, keys, indexes, and the raw/staging/mart layers.

### Implementation
Provide code by file, including:
- config;
- CSV detection;
- loaders;
- transformations;
- DuckDB/PostgreSQL storage;
- MCP server;
- safe query layer;
- example analytical queries.

### Run
Provide exact commands for:
- installation;
- CSV import;
- MCP startup;
- example SQL validation.

### Test
Provide tests and exact test commands.

### Next Step
Show how to extend the system with new SEO report types without rewriting the core.

## What is forbidden
- Do not collapse everything into one table.
- Do not keep the system CSV-only without a SQL layer.
- Do not provide only concepts without code.
- Do not mix raw and mart concerns into one schema.
- Do not expose unrestricted SQL through MCP.
- Do not leave pseudocode instead of a working project structure.

## Extension requirements
Design for future support of:
- merged Metrica + semantic + SERP datasets;
- competitor domain data;
- aggregated KPI calculations;
- large report volumes;
- AI analysis over MCP with minimal token usage.

Start with the architecture, database schema, and module list, then proceed to implementation.
