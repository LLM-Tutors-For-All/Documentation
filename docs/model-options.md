# Model Options

This section documents the brains and knowledge systems used by each course
tutor. Keeping these components separate makes it possible to compare model
providers, retrieval approaches, and course corpora over time.

## Data 8

The current Data 8 tutor combines two components:

- **[GPT Corpus](corpus-options.md):** a local collection and search index of
  Data 8 Spring 2026 course material
- **[OpenAI Brain](openai-options.md):** an OpenAI-compatible model that
  generates answers from retrieved course context

Together they form the tutor's retrieval-augmented generation, or RAG,
pipeline. Future course and model combinations can be added alongside Data 8
without changing the tutor-interface documentation.
