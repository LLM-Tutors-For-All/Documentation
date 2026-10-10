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

## Data 8 options

The Data 8 tutor combines its course corpus with one configured model provider:

- **[GPT Corpus](data8/corpus-options.md):** a local collection and search index
  of Data 8 Spring 2026 course material acting as the knowledge base
- **[OpenRouter Brain](data8/openrouter-options.md):** a selectable model
  accessed through OpenRouter that generates answers from retrieved course
  context; this is the recommended provider
- **[OpenAI Brain](data8/openai-options.md):** direct access to an OpenAI model,
  retained as an alternative provider

The corpus and selected brain form the tutor's retrieval-augmented generation,
or RAG, pipeline. OpenRouter lets the same tutor compare or adopt models from
different developers, while the OpenAI option documents the direct-provider
configuration.
