# Codex Skill: Py/C++ Systems Engineer

This repository contains a Codex-ready skill for Python-first and mixed Python/C++ engineering work.

The skill is now packaged in the directory format Codex expects:

```text
skills/
  py-cpp-systems-engineer/
    SKILL.md
    agents/
      openai.yaml
    references/
      companion-prompts.md
      yandex-serp-parser.md
      seo-csv-sql-mcp-pipeline.md
```

## What Changed

- The main skill is now `skills/py-cpp-systems-engineer/SKILL.md`.
- YAML frontmatter contains only Codex-required `name` and `description`.
- Long specialized prompts were moved to `references/` so Codex loads them only when needed.
- `agents/openai.yaml` was added for Codex UI metadata.
- Legacy standalone markdown prompt files were removed from the active layout.

## What The Skill Does

Use `py-cpp-systems-engineer` for:

- Python applications, modules, scripts, CLIs, services, and pipelines;
- parsers, scrapers, crawlers, and automation;
- CSV, JSON, XML, SQL, logs, and structured data processing;
- DuckDB, SQLite, PostgreSQL, and MCP-style analytics access;
- Python/C++ performance decisions, native extensions, and `pybind11`;
- refactoring, debugging, testing, packaging, and production hardening.

The skill defaults to Python and introduces C++ only when there is a real performance, native integration, or explicit user requirement.

## How To Install In Codex

Copy the whole skill directory, not just `SKILL.md`.

### Windows PowerShell

If `CODEX_HOME` is not set, Codex normally uses `%USERPROFILE%\.codex`.

```powershell
$dest = if ($env:CODEX_HOME) { $env:CODEX_HOME } else { Join-Path $env:USERPROFILE ".codex" }
New-Item -ItemType Directory -Force (Join-Path $dest "skills") | Out-Null
Copy-Item -Recurse -Force ".\skills\py-cpp-systems-engineer" (Join-Path $dest "skills")
```

Expected result:

```text
%USERPROFILE%\.codex\skills\py-cpp-systems-engineer\SKILL.md
%USERPROFILE%\.codex\skills\py-cpp-systems-engineer\agents\openai.yaml
%USERPROFILE%\.codex\skills\py-cpp-systems-engineer\references\...
```

### macOS/Linux

```bash
dest="${CODEX_HOME:-$HOME/.codex}"
mkdir -p "$dest/skills"
cp -R ./skills/py-cpp-systems-engineer "$dest/skills/"
```

Expected result:

```text
~/.codex/skills/py-cpp-systems-engineer/SKILL.md
~/.codex/skills/py-cpp-systems-engineer/agents/openai.yaml
~/.codex/skills/py-cpp-systems-engineer/references/...
```

Restart Codex after copying if the skill list does not refresh automatically.

## How To Trigger It

Examples:

```text
Use py-cpp-systems-engineer. Build a Python parser for this site with tests and CSV export.
```

```text
Use py-cpp-systems-engineer. Refactor this Python package, keep behavior stable, and add regression tests.
```

```text
Use py-cpp-systems-engineer. Build a DuckDB pipeline that imports these SEO CSV reports and exposes safe MCP-style SQL tools.
```

For narrower recurring workflows, see:

- `skills/py-cpp-systems-engineer/references/yandex-serp-parser.md`
- `skills/py-cpp-systems-engineer/references/seo-csv-sql-mcp-pipeline.md`
- `skills/py-cpp-systems-engineer/references/companion-prompts.md`

## Validation

Validate with the Skill Creator helper:

```powershell
python C:\Users\stald\.codex\skills\.system\skill-creator\scripts\quick_validate.py .\skills\py-cpp-systems-engineer
```

If Python is not on PATH, use the Python executable bundled with Codex Desktop.
