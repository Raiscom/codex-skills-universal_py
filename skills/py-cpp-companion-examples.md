## Optional Companion Prompts
Use these in chat when you want to narrow the universal skill to a specific workflow.

### A) Companion prompt for Yandex competitor keyword parser
> Use `py-cpp-systems-engineer`.
> Build a resumable Python project that estimates which queries competitor domains rank for in Yandex by collecting SERP data for a seed keyword list.
> Requirements:
> - Python first, C++ only if a measured bottleneck appears.
> - Input: CSV with seed queries and optional competitor domains.
> - Output: SQL schema + CSV exports for keywords, SERP positions, competitor coverage, URL frequency, and visibility metrics.
> - Architecture: config, fetcher, parser, normalizer, storage, analytics, CLI.
> - Add retries, rate limiting, logging, checkpointing, and tests for parsing/normalization.
> - Prefer DuckDB or SQLite first; justify the choice.
> - Produce file tree, implementation plan, code, and exact run commands.
> - Keep token usage disciplined and avoid boilerplate.

### B) Companion prompt for CSV -> SQL -> MCP analytics pipeline
> Use `py-cpp-systems-engineer`.
> Build a Python data pipeline that ingests multiple CSV reports (metrics, behavior, semantics, technical audits, and competitor reports) into SQL so an AI agent can analyze them through MCP without repeatedly reading raw CSV files.
> Requirements:
> - Detect report types and normalize schemas.
> - Preserve raw landing data, then create normalized tables and analytical views.
> - Use DuckDB locally unless PostgreSQL is clearly justified.
> - Add import metadata, idempotent loading, schema drift handling, and CLI commands.
> - Generate example SQL views for trends, anomalies, landing pages, search queries, competitor comparisons, and technical issue rollups.
> - Output architecture, code, run commands, and guidance for exposing the database to MCP safely.
> - Keep the implementation production-oriented and token-efficient.

