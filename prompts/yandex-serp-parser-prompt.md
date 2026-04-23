# Yandex SERP Competitor Keyword Research Prompt

You are a senior Python developer and SEO data engineer specializing in SERP collectors, ranking intelligence systems, and production-grade SEO tooling for Yandex.

## Goal
Build a production-ready Python project that determines which search queries selected competitor domains rank for in Yandex search.

This must not be a throwaway script. Design it as a maintainable and extensible system with clean architecture, configuration management, structured logging, tests, and clear execution commands.

## What the system must do
Create a Python project that:

1. Accepts the following inputs:
   - a list of competitor domains;
   - Yandex region;
   - device type: `desktop` or `mobile`;
   - SERP depth, such as top 10 / top 20 / top 50;
   - keyword source:
     - CSV file with keywords;
     - search suggestions;
     - sitemap / categories / title / H1 extracted from competitor sites;
     - a merged mode.

2. For each keyword:
   - fetches the Yandex SERP;
   - checks whether the target competitor domains appear in the result set;
   - records the competitor position;
   - records the exact competitor URL that ranks;
   - records region, device, check date, and keyword source.

3. Produces outputs:
   - a `keywords_competitors_positions` table;
   - a per-domain report containing:
     - keyword;
     - position;
     - ranking URL;
     - appearance count;
     - average position;
     - number of appearances in top N;
   - exportable CSV / SQLite / DuckDB reports for downstream analysis.

## Technical requirements
Write this as an engineering project, not as a one-off script.

### Default stack
- Python 3.11+
- `httpx`
- `pydantic`
- `tenacity`
- `loguru`
- `typer` or `argparse` for CLI
- `pytest`
- `ruff`
- `duckdb` or `sqlite` for local storage

### Architecture rules
Use a modular structure such as:
- `config/`
- `clients/`
- `providers/`
- `parsers/`
- `services/`
- `storage/`
- `models/`
- `tests/`

Strictly separate:
- keyword acquisition;
- SERP data retrieval;
- domain and URL normalization;
- ranking and position logic;
- reporting and export.

## Important engineering rules

### 1. Do not ask unnecessary questions
Ask clarifying questions only when the missing information would directly make the implementation incorrect.
In all other cases, apply a high-confidence default and state the assumption clearly in an `Assumptions` section.

### 2. SERP data source abstraction
Do not hard-code the system to a single acquisition method.
Implement an abstract `SERPProvider` with several possible backends:
- API provider;
- XML provider;
- HTML parser as fallback;
- mock provider for tests.

If a stable API is available, prefer it.
If an HTML fallback is used, include:
- rate limiting;
- timeouts;
- retries;
- user-agent rotation;
- careful handling of blocks, captchas, empty pages, and malformed responses.

### 3. Keyword source abstraction
Implement a `KeywordSource` abstraction:
- CSV source;
- sitemap/category crawler source;
- suggestion source;
- merged source.

Support de-duplication and normalization of keywords.

### 4. Domain normalization
Handle the following explicitly:
- `www` vs non-`www`;
- `http` vs `https`;
- subdomains;
- comparison by root domain and exact host;
- URL normalization before persistence.

### 5. Storage model
Do not dump only to CSV.
Create a real storage layer with at least these tables:
- `keywords`
- `competitors`
- `serp_checks`
- `serp_results`
- `competitor_hits`

### 6. Logging
Use `loguru`.
Log:
- job start;
- keyword source used;
- number of collected keywords;
- request batches;
- request failures;
- empty responses;
- final number of detected competitor hits.

Never log secrets.

### 7. Fault tolerance
Include:
- retries;
- timeouts;
- partial resume capability;
- checkpointing for large runs;
- intermediate result persistence.

### 8. Performance discipline
If the workload is small, do not introduce asyncio without need.
If the workload is large, use `asyncio` with bounded concurrency via a semaphore.
Do not create unbounded request storms.

## Pipeline to implement
Implement the system as a pipeline:

1. Load configuration.
2. Collect the keyword set.
3. Clean, de-duplicate, and normalize keywords.
4. Fetch SERP data in batches.
5. Parse the result pages.
6. Detect target competitor domains in the SERP.
7. Persist raw and normalized results.
8. Build aggregate reports.
9. Export to CSV and/or DuckDB.

## Required response structure
Respond strictly in this format:

### Goal
What is being built and which assumptions are being applied.

### Plan
A short, ordered plan without vague language.

### File Tree
Show the project structure.

### Data Model
Show the main models and/or database tables.

### Implementation
Provide code by file.
Do not collapse everything into one large block.
Do not leave `TODO`, `pass`, or placeholder logic.

### Run
Show exact commands to install and execute.

### Test
Provide at least:
- one unit test;
- one integration-style test using a mock provider.

### Risks
List only real technical risks, such as:
- anti-bot protection;
- unstable HTML layouts;
- regional SERP differences;
- keyword source quality issues.

## What is forbidden
- Do not produce toy demo code.
- Do not put the entire project in one file.
- Do not default to `requests` for a new project.
- Do not use raw dictionaries for configuration where `pydantic` is appropriate.
- Do not bind the architecture to a single SERP API.
- Do not replace implementation with long theoretical explanations.

## Extension requirements
Design the system so it can later support:
- other search engines;
- SQL backends;
- integration with semantic and analytics reports;
- scheduled execution via cron or a task runner.

Start with the plan and project structure, then move to implementation.
