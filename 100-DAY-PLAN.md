# 100 Days of Code: Python → AI Applications — Plan

*Repo: ralphp1121.github.io/100daysofcoding (Jekyll, minima theme, deployed via GitHub Actions)*

## Where things stand

- Site is live but unbranded: placeholder title/description in `_config.yml`, default About page, only the stock "welcome to jekyll" post.
- `Python Foundations.pdf` (39 pages, course transcript) shows you've already covered: variables & data types, strings/input/output, conditionals & booleans, lists & loops, dictionaries/JSON/pip, functions, classes & inheritance, files & exceptions, and a first taste of APIs (OpenWeatherMap) and virtual environments.
- Since you're catching the blog up rather than starting from zero, the plan below opens with a **Day 0 recap post** summarizing that existing progress, then **Day 1 begins live, forward-moving content**.

## Phase roadmap (100 days → AI apps)

**Phase 0 — Python Foundations chapter recap (pre-Day 1, own counter)**
Chapter-by-chapter recap of the *Python Foundations* course transcript, before the official 100-day counter starts. See full breakdown below.

**Phase 1 — Practical Python & tooling (Days 1–20)**
Virtual environments, pip & packaging basics, project structure, error handling patterns, unit testing with `pytest`, `argparse` for CLI tools, git/GitHub workflow (branches, commits, PRs), code style (PEP 8, a linter/formatter like `ruff`/`black`).

**Phase 2 — Data & automation (Days 21–40)**
CSV/JSON data wrangling, `pathlib` and file automation scripts, intro `pandas`, basic `sqlite3`, simple web scraping (`requests` + `BeautifulSoup`), consuming a couple more public APIs, small automation projects (file organizer, expense tracker, etc.).

**Phase 3 — Web & interfaces (Days 41–55)**
Building small apps/APIs with Flask or FastAPI, basic HTML templating, wiring a simple front end to a Python backend, deploying a small app (Render/Fly/PythonAnywhere).

**Phase 4 — AI/LLM foundations (Days 56–75)**
Calling LLM APIs (Anthropic/OpenAI) from Python, prompt design basics, structured outputs, embeddings & vector search concepts, light intro to a framework if useful (LangChain or plain SDK calls — your call once you're there).

**Phase 5 — Capstone AI applications (Days 76–100)**
2–4 small AI-powered projects built end to end (e.g., CLI chatbot, document Q&A/RAG tool, summarizer, a simple agent), each wrapped with the Flask/FastAPI skills from Phase 3, deployed, and written up. Day 100: retrospective post linking every project.

*Phase boundaries are guides, not law — slide days around if a topic needs more time.*

## Phase 0 in detail — Python Foundations chapter recap

Source: `Python Foundations.pdf` (39-page course transcript). The course has 7 chapters; two are big enough to split across two days, giving **11 recap days** before Day 1 of the counted 100 begins.

| Day | Chapter | Topics |
|---|---|---|
| 1 | Data Types and Input/Output | variables, `int`/`float`/`str`, `input()`/`print()`, type conversion, string concatenation, comments |
| 2 | Conditionals, Booleans & Imports | `if`/`elif`/`else`, six comparators, `and`/`or`/`not`, booleans, importing modules, the `random` module |
| 3 | Lists & Loops | list creation/indexing, `.append()`/`.remove()`/`del`, `in` operator, `for` loops, `range()`, built-in `sum()`, `break` |
| 4 | Dictionaries & Nested Data | dict creation, keys/values/items, combining lists and dicts, nested dictionaries |
| 5 | JSON, Pip & Virtual Environments | the `json` module, `pip install`, virtual environments, the `requests` package, calling a public API (OpenWeatherMap) |
| 6 | Functions | `def`, parameters, `return`, default arguments, scope |
| 7 | Classes & Objects | `class`, `__init__`, `self`, attributes, methods, instantiating objects |
| 8 | Class Inheritance | subclasses, `super()`, overriding methods, polymorphism |
| 9 | Exceptions | `try`/`except`/`finally`, `raise`, handling bad input, custom exceptions |
| 10 | Reading & Writing Files | `open()`, `read()`/`write()`, the `with` statement, file modes |
| 11 | File Manipulation (capstone) | `os`/`shutil` basics, organizing files programmatically, a mini project combining several chapters |

**Daily loop for Phase 0:**
1. I give you 3 coding challenges scoped to that day's chapter (increasing difficulty: warm-up, applied, mini-project).
2. You work through them on your own.
3. You tell me what you built / where you got stuck.
4. I draft the day's blog post (staged in `_drafts/`, not published) summarizing the topic, your solutions, and what clicked.
5. You review and edit the draft, then move it into `_posts/` (with a real date) and push to publish.

## Cadence & post format

Daily short post, one per coding session:

```markdown
---
layout: post
title: "Day N: <topic>"
date: YYYY-MM-DD
categories: [foundations|tooling|data|web|ai]
---

**Today's focus:** one line on what you set out to do

**What I built:** what you made, with a code snippet

**What I learned:** the concept(s) that clicked (or didn't)

**Next:** what Day N+1 picks up
```

File naming: `_posts/YYYY-MM-DD-day-N-topic-slug.md`

## Site polish

- `_config.yml`: replace placeholder `title`, `email`, `description`, `github_username` with real values.
- `about.markdown`: rewrite — who you are, why 100 days, what "AI applications" means as the end goal.
- Add `categories`/`tags` per phase (foundations, tooling, data, web, ai) so the blog is browsable by topic later.

## GitHub workflow

- One commit per day: `Day N: <topic>` containing the post + that day's code.
- Optional `/projects/day-N-slug/` folder for standalone scripts, linked from the post — keeps the blog root clean and gives you a code portfolio alongside the writing.
- Direct commits to `main` are fine for a solo blog; use a branch+PR per week only if you want the extra git practice.

## Suggested immediate next steps

1. Fix `_config.yml` and `about.markdown` (site polish).
2. Kick off Phase 0, Day 1: Data Types and Input/Output — 3 challenges, then a draft post once you report back.
3. Add a post template file so each new day is copy-paste-fill-in.
4. Once Phase 0 wraps (11 days), Day 1 of the counted 100 begins with Phase 1 (tooling).

Say the word and I can do any of these now.
