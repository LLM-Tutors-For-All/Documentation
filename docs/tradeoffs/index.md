# Architecture tradeoffs

LLM Tutors For All documents not only what the current tutors do, but also
which supporting technologies are worth adopting as the project grows. This
section records the **pros and cons** of several options that come up often in
tutor design: retrieval-augmented generation, LangChain and LangGraph, vLLM,
and key–value caching.

None of these choices is universally best. The right decision depends on how
much course material the tutor has, how much agency the tutoring loop needs,
whether models are hosted or self-served, and how predictable student questions
are in practice.

## Topics

<div class="option-index" markdown>

- **[RAG](rag.md):** grounding answers in a course corpus versus relying on
  the model alone, and when a small corpus limits the payoff
- **[LangChain and LangGraph](langchain-langgraph.md):** a fixed retrieve-then-
  answer pipeline versus an agent that chooses among tools and steps
- **[vLLM](vllm.md):** self-hosted high-throughput inference for open-weight
  models, and the operational cost that comes with it
- **[KV caching](kv-caching.md):** reusing attention state for shared prompts
  and common course context, rather than memorizing specific answers

</div>

## How to read these pages

Each page describes what the technology does in tutor terms, lists advantages
and limitations for this project, and notes the conditions under which it is
likely to help. Where the project already uses a technique (for example, RAG
with a local BM25 corpus), the page also explains what that choice buys and
what it still leaves open.

These notes are decision documentation, not a commitment to adopt every option.
Benchmark work can later test the claims that are measurable, such as latency
and cost under KV caching or retrieval quality under different corpus sizes.
