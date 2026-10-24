# LangChain and LangGraph

LangChain and LangGraph are frameworks for composing LLM applications.
**LangChain** is commonly used to wire prompts, retrievers, tools, and model
calls into a pipeline. **LangGraph** builds on that idea with explicit state
and branching: the system can choose the next step instead of always running
the same sequence.

## Two orchestration styles

### Linear sequence

A fixed tutoring loop looks like:

1. Receive the student question
2. Look up the corpus
3. Read the retrieved chunks
4. Generate a response (and optionally a follow-up action)

Every turn follows the same path. This matches a simple RAG tutor: retrieve,
then generate. Behavior is easy to reason about, test, and benchmark.

### Agent with options

An agentic loop gives the model a set of allowed actions—search the corpus,
reread a passage, ask a clarifying question, check a calculation, refuse to
solve the problem outright—and lets it pick which to run next. LangGraph is
often used for this style because control flow is a graph of states rather
than a single chain.

Agency can help when the right next step depends on the conversation. It also
adds failure modes: looping, unnecessary tool calls, and harder-to-reproduce
traces.

## Advantages

**Linear (chain-style) orchestration**

- Predictable cost and latency per turn
- Straightforward logging and evaluation
- Easier to keep pedagogical guardrails consistent
- Enough for many course tutors that only need retrieve-then-answer

**Agentic (graph-style) orchestration**

- Can recover when first retrieval misses
- Can choose different tools for different question types
- Fits multi-step tutoring such as diagnose mistake → hint → check understanding
- Makes complex workflows explicit as states and edges

## Limitations

**Linear**

- Cannot adapt mid-turn if the first plan was wrong
- Harder to express branching office-hours behavior without bespoke code

**Agentic**

- Higher and less predictable token use
- Harder to reproduce and score in benchmarks
- Framework abstractions can obscure what the tutor actually did
- Risk of over-engineering a problem that a fixed RAG loop already solves

## When each is likely to help

Prefer a **linear** pipeline while the tutor’s job is “retrieve course context,
then respond with tutoring constraints.” That is the current Data 8 shape.

Consider **LangGraph-style agency** when product requirements need branching
behavior that is painful to hard-code: multi-tool workflows, conditional
escalation, or multi-step diagnosis with explicit state. Adopt it when those
needs are clear, not because an agent sounds more advanced.

## Project stance

Framework choice is secondary to tutoring behavior. A small custom pipeline is
acceptable if it stays readable. LangChain is useful when shared components
(retrievers, prompt templates, providers) reduce duplication. LangGraph is
worth evaluating when the tutor needs real decision points between steps, not
only a fixed retrieve → read → answer sequence.
