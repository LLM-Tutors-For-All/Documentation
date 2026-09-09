# Data 8 Bot: Getting Started

This guide prepares and runs the current Data 8 tutor. Complete it before
starting the local, Discord, or Slack tutor option.

![Course files are indexed locally, retrieved for a question, and sent to the tutoring engine before reaching each interface.](assets/tutor-flow.svg)

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

Continue with the [local interactive tutor](local-tutor.md), the
[Discord integration](discord.md), or the [Slack integration](slack.md).
