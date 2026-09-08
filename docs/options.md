# Tutor Options

The project currently runs one Data 8 tutor through three interfaces. Each
interface uses the same course corpus, retrieval system, and tutoring engine.

## Choose an interface

### Local CLI

Run one-shot questions or an interactive chat directly in a terminal. This is
the simplest option for development, retrieval testing, and staff-mode access.

[Set up the local tutor](local-tutor.md)

### Discord

Let students ask questions through mentions, direct messages, or the `/tutor`
slash command in a Discord server.

[Set up Discord](discord.md)

### Slack

Let students ask questions through mentions, direct messages, or `/tutor` in a
Slack workspace using Socket Mode.

[Set up Slack](slack.md)

All three tutor options currently use the same
[GPT corpus](gpt-corpus.md) and [OpenAI brain](openai-brain.md).
