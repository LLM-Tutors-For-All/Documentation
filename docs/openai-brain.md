# OpenAI Brain

The current tutor brain sends retrieved course context and the learner's
question to an OpenAI-compatible chat completions API.

## Configuration

Add an API key to `.env`:

```dotenv
OPENAI_API_KEY=your-api-key
```

The default model is `gpt-4o-mini`. Override it when needed:

```dotenv
OPENAI_MODEL=gpt-4o-mini
```

The project also supports a custom OpenAI-compatible endpoint:

```dotenv
OPENAI_BASE_URL=https://your-compatible-endpoint.example/v1
```

## How it is used

For each question, the tutor:

1. Retrieves relevant chunks from the GPT corpus.
2. Adds those chunks and recent conversation history to the prompt.
3. Requests a response from the configured chat model.
4. Returns the answer with its course source files.

The same brain is shared by the local CLI, Discord, and Slack tutor options.
Other model brains can be documented alongside this one after they are
implemented.
