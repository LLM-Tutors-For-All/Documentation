# Data 8 GPT Corpus

The GPT corpus is the local knowledge component of the Data 8 tutor. It grounds
answers in UC Berkeley Data 8 Spring 2026 course material instead of asking the
model to rely only on its pretrained knowledge.

## What it contains

The Markdown corpus under `gpt_corpus/data8/sp26/` includes:

- Lectures
- Assignments and projects
- Textbook material
- Discussion and tutoring worksheets
- Exams

Student mode excludes solution-only files and strips solution sections from
student-facing material.

## How indexing works

```bash
python -m tutor ingest
```

The ingestion process splits the course files into chunks of up to roughly
3,500 characters and stores a local BM25 index under `tutor_data/`. BM25 ranks
chunks by how well their terms match a student's question.

The default index:

- Runs locally
- Does not require an API key
- Does not create retrieval API charges
- Can be inspected with `python -m tutor retrieve "question"`

## Optional embeddings

```bash
python -m tutor ingest --embed
```

This embeds the corpus with OpenAI's `text-embedding-3-small`. Each question is
also embedded, and its semantic ranking is combined with BM25.

Embedding-assisted retrieval can find conceptually similar passages when the
question and course material use different words. It also adds an initial
corpus-embedding cost and an embedding request for each new question.

## Advantages

- Keeps the source course material local
- Grounds answers in identifiable course files
- Avoids hosted vector-database infrastructure
- Works with free local BM25 retrieval by default
- Separates student and staff content
- Can be rebuilt when course material changes

## Limitations

- Exact-term BM25 retrieval may miss conceptually similar wording
- Embeddings improve semantic matching but add API cost
- Corpus quality depends on the completeness and conversion of source material
- The local index must be rebuilt after course files change
- This corpus currently covers only Data 8 Spring 2026

## RAG versus the local corpus

The corpus and RAG are not alternatives:

1. The **corpus** stores the course knowledge.
2. **Retrieval** selects relevant chunks using BM25 and optional embeddings.
3. The **OpenAI brain** generates an answer from those chunks.
4. The complete retrieve-then-generate process is **RAG**.

The default setup is still RAG even though its corpus and BM25 index are local.
