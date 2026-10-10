# Data 8 OpenRouter Brain

The Data 8 tutor uses [OpenRouter](https://openrouter.ai/) as its recommended
model provider. OpenRouter exposes models from multiple developers through one
API, so the tutor's model can be changed without replacing its response
pipeline. The default model is `openai/gpt-4o-mini`.

## Configuration

Create an API key in your
[OpenRouter account](https://openrouter.ai/settings/keys), then configure the
project's `.env` file:

```dotenv
LLM_PROVIDER=openrouter
OPENROUTER_API_KEY=your-api-key
OPENROUTER_MODEL=openai/gpt-4o-mini
OPENROUTER_APP_NAME=LLM Tutors For All
```

Keep the API key private and never commit `.env`.

`OPENROUTER_MODEL` can be set to another identifier from the
[OpenRouter model directory](https://openrouter.ai/models). Model capabilities,
context limits, availability, and pricing vary, so verify that a model supports
the tutor's requirements before selecting it.

Optional settings include:

```dotenv
# OPENROUTER_EMBEDDING_MODEL=openai/text-embedding-3-small
# OPENROUTER_BASE_URL=https://openrouter.ai/api/v1
# OPENROUTER_SITE_URL=https://your-app.example
```

- `OPENROUTER_EMBEDDING_MODEL` selects a model for optional semantic retrieval.
- `OPENROUTER_BASE_URL` overrides the API endpoint.
- `OPENROUTER_SITE_URL` identifies the deployment to OpenRouter.
- `OPENROUTER_APP_NAME` supplies the application name shown to OpenRouter.

## How the brain is used

For each question, the tutor:

1. Retrieves relevant course chunks from the local Data 8 index.
2. Combines them with tutor instructions, the question, and recent chat
   history.
3. Sends that input to the configured OpenRouter model.
4. Returns the generated answer and relevant course sources.

The local CLI, Discord, and Slack tutor options all use this same configured
brain.

## Changing models

Only the model identifier needs to change:

```dotenv
OPENROUTER_MODEL=provider/model-name
```

Restart a running tutor after changing `.env`. Using one provider interface
makes it easier to test models under the same tutor prompt, retrieval process,
and application code.

Changing models can still affect answer quality, context capacity, latency,
availability, and cost. A model name should therefore be recorded alongside
any benchmark or deployment result.

## Model costs

OpenRouter charges separately for input and output tokens. Input includes the
tutor instructions, retrieved course passages, the student's question, and
recent conversation history. Output is the model's generated response and, for
some models, may also include billed reasoning tokens.

The following selection includes four of OpenRouter's most-used models by token
volume on October 6, 2026, plus this project's default model. Popularity
measures usage through OpenRouter; it does not measure tutoring quality.

- **[DeepSeek V4.1 Flash](https://openrouter.ai/deepseek/deepseek-v4.1-flash)**
  (`deepseek/deepseek-v4.1-flash`): **$0.045 per million input tokens** and
  **$1.20 per million output tokens**
- **[GLM 5.3 Flash](https://openrouter.ai/z-ai/glm-5.3-flash)**
  (`z-ai/glm-5.3-flash`): **$0.0214 per million input tokens** and **$0.50 per
  million output tokens**
- **[MiMo-V2.6-Flash](https://openrouter.ai/xiaomi/mimo-v2.6-flash)**
  (`xiaomi/mimo-v2.6-flash`): **$0.10 per million input tokens** and **$0.28
  per million output tokens**
- **[GPT-6 Luna](https://openrouter.ai/openai/gpt-6-luna)**
  (`openai/gpt-6-luna`): **$0.10 per million input tokens** and **$0.50 per
  million output tokens**
- **[GPT-4o mini](https://openrouter.ai/openai/gpt-4o-mini)**
  (`openai/gpt-4o-mini`, the current default): **$0.15 per million input
  tokens** and **$0.60 per million output tokens**

For illustration, a turn containing 8,000 input tokens and 500 output tokens
would cost approximately:

- DeepSeek V4.1 Flash: **$0.00096**
- GLM 5.3 Flash: **$0.00042**
- MiMo-V2.6-Flash: **$0.00094**
- GPT-6 Luna: **$0.00105**
- GPT-4o mini: **$0.00150**

These are estimates based on the listed text-token rates, checked October 7,
2026. They exclude cache pricing, embeddings, web search, provider-routing
preferences, and other model-specific charges. OpenRouter rankings and prices
change over time, so check the linked model pages before budgeting or reporting
benchmark costs.

## Optional embeddings

The default BM25 index is local and does not need an API key. To add semantic
retrieval, select an embedding model and rebuild the index:

```dotenv
OPENROUTER_EMBEDDING_MODEL=openai/text-embedding-3-small
```

```bash
python -m tutor ingest --embed
```

Embedding requests have their own availability and pricing. Check the selected
model's OpenRouter page before use.

## OpenAI fallback

Direct OpenAI access remains supported:

```dotenv
LLM_PROVIDER=openai
OPENAI_API_KEY=your-api-key
OPENAI_MODEL=gpt-4o-mini
# OPENAI_EMBEDDING_MODEL=text-embedding-3-small
# OPENAI_BASE_URL=
```

Use one provider configuration at a time. An OpenRouter key cannot be used as
an OpenAI key, and a ChatGPT subscription does not include API access.

## Advantages

- One API configuration can access models from multiple developers
- Models can be changed without modifying tutor code
- No local model-serving infrastructure is required
- The same provider configuration is shared by all tutor interfaces
- Direct OpenAI access remains available as a fallback

## Limitations

- Generated answers require an external provider and API key
- Price, context limits, and capabilities differ by selected model
- Model availability and routing can change
- Latency depends on OpenRouter and the underlying model provider
- Course context and student questions are sent to external services
- Fully local generation is not currently implemented
