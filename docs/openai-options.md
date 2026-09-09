# Data 8 OpenAI Brain

The current Data 8 tutor uses an OpenAI-compatible Chat Completions API to
generate responses from retrieved course context. Its default model is
`gpt-4o-mini`.

## Configuration

Create a key on the
[OpenAI API key page](https://platform.openai.com/api-keys) and add it to the
project's `.env` file:

```dotenv
OPENAI_API_KEY=your-api-key
OPENAI_MODEL=gpt-4o-mini
```

The API key is separate from a ChatGPT subscription. Keep it private and never
commit `.env`.

`OPENAI_MODEL` is optional. The project also accepts `OPENAI_BASE_URL` for an
OpenAI-compatible endpoint.

## How the brain is used

For each question, the tutor:

1. Retrieves up to eight relevant course chunks by default.
2. Combines them with tutor instructions, the question, and recent chat
   history.
3. Sends that input to the configured model.
4. Returns the generated answer and course source files.

The local CLI, Discord, and Slack tutor options all use this same brain.

## Token use

Input tokens include:

- Tutor system instructions
- Retrieved course chunks
- The student's question
- Recent conversation history

Output tokens are the generated response. Longer context and conversations
increase cost.

The current code does not save OpenAI's returned `usage` values, so measured
per-question token totals are not available yet.

## Current cost

OpenAI lists the standard text rates for
[`gpt-4o-mini`](https://developers.openai.com/api/docs/models/gpt-4o-mini) as:

- **Input:** $0.15 per 1 million tokens
- **Cached input:** $0.075 per 1 million tokens
- **Output:** $0.60 per 1 million tokens

The optional
[`text-embedding-3-small`](https://developers.openai.com/api/docs/models/text-embedding-3-small)
retrieval model is listed at **$0.02 per 1 million input tokens**.

Prices were checked on September 9, 2026 and may change. Verify the official
model pages before reporting benchmark costs.

For illustration, 8,000 input tokens and 500 output tokens at these
`gpt-4o-mini` rates would cost about **$0.0015**. This is an example, not a
measurement of the Data 8 tutor.

## Advantages

- Low listed token price for the default model
- Simple hosted API with no local model infrastructure
- Shared implementation across local, Discord, and Slack tutors
- Model can be changed through an environment variable
- Supports an OpenAI-compatible custom endpoint

## Limitations

- Requires an external service and API key
- Usage creates variable operating cost
- Availability and latency depend on the provider
- Course context and questions are sent to the configured API
- Pricing and model behavior can change
- The current tutor does not record token usage for benchmarking
- Fully local generation is not currently implemented
