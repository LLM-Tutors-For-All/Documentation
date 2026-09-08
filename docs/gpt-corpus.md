# GPT Corpus

The GPT corpus is the tutor's course-knowledge layer. The current implementation
uses UC Berkeley Data 8 Spring 2026 materials stored as Markdown under
`gpt_corpus/data8/sp26/`.

## Included material

- Lectures
- Assignments and projects
- Textbook material
- Discussion and tutoring worksheets
- Exams

## Indexing

Run:

```bash
python -m tutor ingest
```

The ingestion process discovers the Markdown files, divides them into chunks,
and writes a local search index under `tutor_data/`. The default index uses
BM25 and does not require an API key.

For embedding-assisted retrieval:

```bash
python -m tutor ingest --embed
```

This adds OpenAI embeddings and combines semantic and BM25 retrieval.

## Student and staff content

Student mode excludes solution files and strips solution blocks from student
materials. The local CLI can enable staff mode, while Discord and Slack always
use student mode.

Future classes should receive separate corpora, ingestion checks, and
evaluations rather than being mixed into the Data 8 corpus.
