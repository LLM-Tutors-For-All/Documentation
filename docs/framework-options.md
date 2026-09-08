# Framework Options

Framework options describe the components inside a tutor deployment: the
course knowledge it retrieves and the model service that generates responses.
They are separate from the local, Discord, and Slack interfaces.

## Currently implemented

### GPT Corpus

The current corpus contains UC Berkeley Data 8 Spring 2026 course material. It
is converted to Markdown and indexed locally for retrieval.

[Read about the GPT corpus](gpt-corpus.md)

### OpenAI Brain

The current tutoring engine uses an OpenAI-compatible chat completions API,
with `gpt-4o-mini` as its default model.

[Read about the OpenAI brain](openai-brain.md)

Additional course corpora and model brains can be added here as they are
implemented and evaluated.
