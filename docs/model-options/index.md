# Model Options

LLM Tutors For All separates each tutor's **knowledge base** from its
**brain** so that course information can be evaluated independently from the
model that generates responses.

## Knowledge base versus brain

- The **knowledge base**, or corpus, contains the course information available
  to the tutor. Its local search index retrieves relevant material for each
  question.
- The **brain** is the configured language model. It receives the question,
  tutoring instructions, and retrieved course context, then generates the
  response.

Keeping them separate makes it possible to compare course corpora, retrieval
approaches, and model providers in controlled combinations.

## Data 8 brain

The current Data 8 tutor combines these two components:

- **[GPT Corpus](data8/corpus-options.md):** a local collection and search index
  of Data 8 Spring 2026 course material acting as the knowledge base
- **[OpenAI Brain](data8/openai-options.md):** an OpenAI-compatible model that
  generates answers from retrieved course context acting as the brain

Together they form the tutor's retrieval-augmented generation, or RAG,
pipeline. Future course and model combinations can be added alongside Data 8
without restructuring the documentation.
