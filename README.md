# Codex Skills Pack for Python, C++, SEO Parsers, and SQL/MCP Analytics

This repository contains a practical set of reusable **Codex-oriented skills and task prompts** for engineering work in Python and C++, with a focus on:

- production-grade Python development;
- mixed Python/C++ architecture;
- SEO data collection and parser development;
- CSV-to-SQL ingestion pipelines;
- MCP-based analytical access for AI over structured data.

The goal of this pack is to make Codex behave more like a disciplined engineer: plan first, write modular code, avoid unnecessary token waste, and produce code that is easier to run, test, extend, and maintain.

---

## Why this repository exists

Large coding models often produce decent code, but without a strong task frame they may:

- generate one-file demo scripts instead of maintainable projects;
- ask unnecessary questions;
- over-explain instead of implementing;
- ignore testing, logging, dependency discipline, or schema design;
- waste context on repetitive instructions.

This repository solves that by separating the workflow into:

1. **A universal base skill** for broad engineering tasks.
2. **Companion examples** that show how to invoke that skill in practice.
3. **Specialized prompts** for narrow, recurring tasks such as SEO SERP parsing or CSV → SQL → MCP analytics.

---

## Repository structure

```text
skills/
  Universal_Py_Cpp_Codex_SKILL_v1.1.0.md
  py-cpp-companion-examples.md

prompts/
  yandex-serp-parser-prompt.md
  seo-csv-sql-mcp-pipeline-prompt.md
```

---

## What each file is for

### `skills/Universal_Py_Cpp_Codex_SKILL_v1.1.0.md`

This is the **main universal Codex skill**.

Use it when the task is broad or engineering-heavy, for example:

- building Python tools or services;
- writing parsers or crawlers;
- designing ingestion pipelines;
- deciding between Python and C++;
- refactoring a codebase;
- improving performance;
- building structured, testable project layouts.

This skill defines the expected engineering behavior:

- clear intake and assumptions;
- minimal but sufficient clarification;
- modular architecture;
- token-efficient output;
- typed Python code;
- logging standards;
- async decision rules;
- dependency discipline;
- testing expectations;
- quality checklist before delivery.

In short: this file is the **default engineering brain**.

---

### `skills/py-cpp-companion-examples.md`

This file contains **example companion prompts**.

It is intentionally separated from the main skill so the base skill stays compact and token-efficient.

Purpose of this file:

- show how to invoke the universal skill in real scenarios;
- provide examples of user task framing;
- avoid bloating the main skill with usage samples.

This file is not the skill itself.  
It is a **usage reference**.

---

### `prompts/yandex-serp-parser-prompt.md`

This is a **specialized prompt** for building a Python system that finds **which keywords competitor domains rank for in Yandex search**.

Use it when you want Codex to focus narrowly on:

- Yandex SERP collection;
- competitor domain tracking;
- keyword sources;
- position detection;
- regional/device-specific ranking analysis;
- export into CSV / SQLite / DuckDB;
- extensible SEO data architecture.

This is useful when the universal skill is too broad and you want to force a very specific implementation direction.

In short: this prompt is for **SEO competitor ranking research tooling**.

---

### `prompts/seo-csv-sql-mcp-pipeline-prompt.md`

This is a **specialized prompt** for building a pipeline that ingests large SEO and analytics CSV reports into SQL and exposes them to AI through MCP.

Use it when the task is about:

- importing CSV reports from Yandex Metrica or other SEO sources;
- schema normalization;
- raw/staging/mart SQL layers;
- analytical views;
- safe read-only query interfaces;
- reducing token waste by making AI work over SQL summaries instead of raw CSV.

This prompt is especially useful when you want AI to analyze large report sets without repeatedly reading giant files.

In short: this prompt is for **structured SEO analytics infrastructure**.

---

## How to use this repository

### Option 1 — Use the universal skill as the default
Use `skills/Universal_Py_Cpp_Codex_SKILL_v1.1.0.md` as the main skill when the task is still open-ended.

Examples:

- “Build a parser for this website.”
- “Refactor this Python project.”
- “Should this part stay in Python or move to C++?”
- “Design a maintainable data ingestion architecture.”

### Option 2 — Use a specialized prompt for narrow tasks
When the task is already known and highly specific, use the corresponding prompt from `prompts/`.

Examples:

- Need Yandex competitor keyword tracking → use `prompts/yandex-serp-parser-prompt.md`
- Need CSV → SQL → MCP analytics pipeline → use `prompts/seo-csv-sql-mcp-pipeline-prompt.md`

### Option 3 — Use both together
A practical pattern is:

1. keep the universal skill active as the main engineering behavior;
2. add one specialized prompt in the chat for the exact current task.

That gives you both:

- stable coding discipline;
- task-specific implementation focus.

---

## Recommended usage pattern

For most projects, the best workflow is:

1. Start with the universal skill.
2. Use companion examples if you need a model for phrasing the request.
3. Add a specialized prompt when the task enters a narrow domain.
4. Keep outputs modular: config, services, models, storage, tests.
5. Prefer reproducible pipelines over ad-hoc scripts.

---

## Who this is for

This repository is useful for:

- Python developers;
- SEO engineers;
- data engineers;
- automation developers;
- parser/crawler builders;
- analysts who want AI to work over SQL instead of raw files;
- users who want Codex to behave like a disciplined implementation partner rather than a generic chatbot.

---

## Design principles

This pack is built around several principles:

- **Engineering-first** — code should be runnable, testable, and maintainable.
- **Token economy** — save context where possible, but not at the cost of output quality.
- **Modularity** — separate configuration, parsing, storage, business logic, and tests.
- **Reproducibility** — use structured dependencies, pinned versions where appropriate, and explicit run commands.
- **Safety** — avoid unnecessary destructive actions, unsafe SQL, or secret leakage.
- **Extensibility** — solutions should be easy to adapt to new providers, new report types, or larger pipelines.

---

## Notes

- The universal skill is the main reusable asset.
- The companion examples are support material, not system instructions.
- The specialized prompts are narrow execution templates, not replacements for the universal skill.
- A future improvement is to convert the specialized prompts into standalone skills.

---

## Summary

This repository provides:

- one **universal engineering skill**;
- one **companion example file**;
- two **narrow task prompts** for recurring SEO/data-engineering work.

Use the universal skill as the foundation.  
Use the specialized prompts when you need Codex to move in a very specific implementation direction.

---

# Русская версия

# Набор Skills и Prompts для Codex: Python, C++, SEO-парсеры и SQL/MCP-аналитика

Этот репозиторий содержит практический набор **скиллов и рабочих промптов для Codex**, ориентированных на разработку на Python и C++, с упором на:

- production-подход к Python-разработке;
- смешанную архитектуру Python/C++;
- сбор SEO-данных и разработку парсеров;
- пайплайны загрузки CSV в SQL;
- доступ ИИ к аналитическим данным через MCP.

Цель этого набора — заставить Codex работать не как “генератор кода наугад”, а как более дисциплинированный инженер: сначала планировать, потом писать модульный код, не тратить лишние токены и выдавать решения, которые проще запускать, тестировать, расширять и поддерживать.

---

## Зачем нужен этот репозиторий

Большие кодовые модели часто пишут неплохой код, но без жёсткой рамки задачи они склонны:

- генерировать однофайловые demo-скрипты вместо нормального проекта;
- задавать лишние вопросы;
- слишком много объяснять вместо реализации;
- игнорировать тесты, логирование, зависимости и схему данных;
- тратить контекст на повторяющиеся инструкции.

Этот репозиторий решает проблему через разделение на несколько уровней:

1. **Универсальный базовый skill** для широких инженерных задач.
2. **Companion examples** — примеры того, как этот skill вызывать на практике.
3. **Узкие промпты** для повторяющихся задач, например:
   - парсинг выдачи Яндекса и анализ конкурентов;
   - пайплайн CSV → SQL → MCP для аналитики.

---

## Структура репозитория

```text
skills/
  Universal_Py_Cpp_Codex_SKILL_v1.1.0.md
  py-cpp-companion-examples.md

prompts/
  yandex-serp-parser-prompt.md
  seo-csv-sql-mcp-pipeline-prompt.md
```

---

## Для чего нужен каждый файл

### `skills/Universal_Py_Cpp_Codex_SKILL_v1.1.0.md`

Это **главный универсальный skill для Codex**.

Используй его, когда задача широкая или инженерно сложная, например:

- разработка Python-инструментов и сервисов;
- написание парсеров и crawler-систем;
- проектирование ingestion-пайплайнов;
- выбор между Python и C++;
- рефакторинг проекта;
- оптимизация производительности;
- построение нормальной структуры проекта с тестами.

Этот skill задаёт ожидаемое инженерное поведение:

- понятный intake и assumptions;
- минимум лишних уточнений;
- модульная архитектура;
- экономия токенов без потери качества;
- типизированный Python-код;
- стандарты логирования;
- правила выбора async;
- дисциплина зависимостей;
- требования к тестам;
- чек-лист качества перед выдачей результата.

Иными словами: это **базовый инженерный мозг**.

---

### `skills/py-cpp-companion-examples.md`

Этот файл содержит **примеры companion prompts**.

Он специально вынесен отдельно, чтобы основной skill оставался компактным и не раздувал системный контекст.

Назначение файла:

- показать, как использовать универсальный skill на реальных задачах;
- дать примеры формулировки запросов;
- не перегружать основной skill примерами использования.

Это не сам skill.  
Это **файл-пример по использованию**.

---

### `prompts/yandex-serp-parser-prompt.md`

Это **узкоспециализированный промпт** для разработки Python-системы, которая определяет, **по каким ключам конкуренты ранжируются в Яндексе**.

Его стоит использовать, когда нужно, чтобы Codex сосредоточился именно на:

- снятии SERP Яндекса;
- отслеживании доменов конкурентов;
- источниках ключевых запросов;
- определении позиций;
- анализе по региону и устройству;
- выгрузке в CSV / SQLite / DuckDB;
- расширяемой SEO-архитектуре.

Он полезен, когда универсальный skill слишком широкий и нужно жёстко задать одно направление реализации.

Иными словами: этот промпт нужен для **инструмента исследования позиций конкурентов в поиске Яндекса**.

---

### `prompts/seo-csv-sql-mcp-pipeline-prompt.md`

Это **узкоспециализированный промпт** для разработки системы, которая загружает большие SEO- и аналитические CSV-отчёты в SQL и даёт ИИ доступ к ним через MCP.

Его стоит использовать, когда задача связана с:

- импортом CSV-отчётов из Яндекс Метрики и других SEO-источников;
- нормализацией схем;
- построением raw/staging/mart слоя;
- аналитическими представлениями;
- безопасным read-only доступом через SQL;
- снижением расхода токенов за счёт того, что ИИ работает не с сырыми CSV, а с SQL-сводками и агрегатами.

Этот промпт особенно полезен, когда нужно анализировать большие массивы отчётов и не хочется каждый раз “скармливать” ИИ огромные файлы.

Иными словами: этот промпт нужен для **построения аналитической SEO-инфраструктуры поверх SQL и MCP**.

---

## Как использовать этот репозиторий

### Вариант 1 — использовать универсальный skill как основной
Используй `skills/Universal_Py_Cpp_Codex_SKILL_v1.1.0.md` как главный skill, когда задача ещё широкая.

Примеры:

- “Сделай парсер этого сайта.”
- “Отрефактори этот Python-проект.”
- “Оставить эту часть на Python или вынести в C++?”
- “Спроектируй нормальную архитектуру ingestion-пайплайна.”

### Вариант 2 — использовать узкий промпт для конкретной задачи
Когда задача уже точно определена, бери подходящий промпт из `prompts/`.

Примеры:

- нужен анализ ключей/позиций конкурентов в Яндексе → `prompts/yandex-serp-parser-prompt.md`
- нужен пайплайн CSV → SQL → MCP → `prompts/seo-csv-sql-mcp-pipeline-prompt.md`

### Вариант 3 — использовать оба вместе
Практический рабочий паттерн такой:

1. универсальный skill остаётся основным инженерным поведением;
2. в чат дополнительно вставляется один узкий промпт под текущую задачу.

Так ты получаешь сразу две вещи:

- стабильную инженерную дисциплину;
- фокус на конкретной реализации.

---

## Рекомендуемый способ работы

Для большинства проектов оптимальный порядок такой:

1. Начать с универсального skill.
2. Смотреть companion examples, если нужен образец формулировки задачи.
3. Добавлять узкий промпт, когда работа уходит в конкретную предметную область.
4. Держать результат модульным: config, services, models, storage, tests.
5. Предпочитать воспроизводимые пайплайны, а не одноразовые скрипты.

---

## Для кого это полезно

Этот репозиторий подойдёт:

- Python-разработчикам;
- SEO-специалистам с техническим уклоном;
- data engineers;
- разработчикам автоматизации;
- тем, кто пишет парсеры и crawler-системы;
- аналитикам, которые хотят, чтобы ИИ работал поверх SQL, а не сырых файлов;
- тем, кто хочет использовать Codex как дисциплинированного инженерного помощника, а не просто как чат-бота.

---

## Основные принципы

Этот набор построен на нескольких принципах:

- **Engineering-first** — код должен запускаться, тестироваться и поддерживаться.
- **Token economy** — экономить контекст там, где это возможно, но не в ущерб качеству результата.
- **Modularity** — разделять конфиг, парсинг, хранение, бизнес-логику и тесты.
- **Reproducibility** — использовать управляемые зависимости, явные команды запуска и воспроизводимый пайплайн.
- **Safety** — избегать опасных действий, небезопасного SQL и утечки секретов.
- **Extensibility** — решения должны легко расширяться под новые источники, новые отчёты и более крупные пайплайны.

---

## Примечания

- Универсальный skill — это основной переиспользуемый артефакт.
- Companion examples — это вспомогательный материал, а не системные инструкции.
- Узкие промпты — это шаблоны под конкретные задачи, а не замена универсального skill.
- Следующее логичное улучшение — превратить узкие промпты в отдельные standalone skills.

---

## Краткий итог

Этот репозиторий содержит:

- один **универсальный инженерный skill**;
- один **файл с примерами использования**;
- два **узких промпта** для повторяющихся SEO/data-engineering задач.

Используй универсальный skill как основу.  
Используй узкие промпты, когда нужно направить Codex в строго определённую реализацию.
