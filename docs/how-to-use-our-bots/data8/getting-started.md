# Data 8 Bot: Getting Started

This guide prepares and runs the current Data 8 tutor. Complete it before
starting the local, Discord, or Slack tutor option.

## Current course

![Data 8 course logo.](../../assets/gallery/data8.jpg){ .course-logo-large }

The tutor is grounded in UC Berkeley Data 8 Spring 2026 lectures, assignments,
textbook material, worksheets, and exams.

## How it works

<div class="outline-grid" markdown>

<div class="outline-card" markdown>
:material-bookshelf:{ .outline-card__icon }

### Course corpus

Data 8 lectures, assignments, and references provide the tutor's grounded
knowledge.
</div>

<div class="outline-card" markdown>
:material-database-search:{ .outline-card__icon }

### Local retrieval

BM25, with optional embeddings, selects course passages related to each
question.
</div>

<div class="outline-card" markdown>
:material-brain:{ .outline-card__icon }

### Tutor brain

The OpenAI-compatible model uses retrieved context to construct a focused
answer.
</div>

<div class="outline-card" markdown>
:material-message-processing-outline:{ .outline-card__icon }

### Tutor interfaces

The same response engine supports the local CLI, Discord, and Slack bodies.
</div>

</div>

## Requirements

- Python 3
- A clone of the
  [LLM-Tutors-For-All repository](https://github.com/LLM-Tutors-For-All/LLM-Tutors-For-All)
- An OpenAI API key for generated answers

## 1. Create the environment

Open a terminal in the project repository:

=== "Windows PowerShell"

    ```powershell
    python -m venv .venv
    .\.venv\Scripts\Activate.ps1
    pip install -r requirements.txt
    Copy-Item .env.example .env
    ```

=== "macOS or Linux"

    ```bash
    python -m venv .venv
    source .venv/bin/activate
    pip install -r requirements.txt
    cp .env.example .env
    ```

## 2. Configure the model

Open `.env` and add your API key:

```dotenv
OPENAI_API_KEY=your-api-key
OPENAI_MODEL=gpt-4o-mini
```

`OPENAI_MODEL` is optional and defaults to `gpt-4o-mini`. The project also
accepts `OPENAI_BASE_URL` for an OpenAI-compatible endpoint.

!!! warning "Keep credentials private"
    Never commit `.env` or paste API and bot tokens into documentation, issues,
    or chat messages.

## 3. Build the local index

```bash
python -m tutor ingest
python -m tutor status
```

The default index uses local BM25 retrieval and does not call OpenAI. To add
OpenAI embeddings and combine them with BM25 retrieval:

```bash
python -m tutor ingest --embed
```

Rebuild the index whenever course files in `gpt_corpus/` change.

## 4. Verify retrieval and answers

Check retrieval without calling the LLM:

```bash
python -m tutor retrieve "How do I filter rows of a table?"
```

Then ask a generated question:

```bash
python -m tutor ask "I'm stuck on using tbl.where"
```

Continue with the
[local interactive tutor](../../tutor-options/interfaces/local-cli.md), the
[Discord integration](../../tutor-options/interfaces/discord.md), or the
[Slack integration](../../tutor-options/interfaces/slack.md).
