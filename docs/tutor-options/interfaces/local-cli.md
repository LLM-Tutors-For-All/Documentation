# Local CLI Tutor

The command-line interface is the fastest way to test the tutor without
configuring a chat platform. First complete
[Data 8 Getting Started](../../how-to-use-our-bots/data8/getting-started.md).

## Use it in the local CLI

### One question

```bash
python -m tutor ask "How do I use tbl.where?"
```

The command retrieves relevant course chunks, generates one response, lists its
source files, and exits.

### Interactive chat

```bash
python -m tutor chat
```

The chat remembers recent turns so you can ask follow-up questions. Enter
`/quit` to exit.

### Inspect retrieval

Use `retrieve` to see which course chunks match a question without calling the
LLM:

```bash
python -m tutor retrieve "How do I filter rows of a table?"
```

Change the number of returned chunks with `-k`:

```bash
python -m tutor retrieve "What is bootstrapping?" -k 5
```

### Staff mode

Authorized course staff can include solution materials:

```bash
python -m tutor ask "Explain this solution" --staff
python -m tutor chat --staff
```

Within interactive chat, `/staff` toggles staff mode. Discord and Slack always
remain in student mode.
