# vLLM

[vLLM](https://docs.vllm.ai/) is an inference engine for serving large language
models efficiently, especially open-weight models on your own GPUs. It focuses
on high throughput and memory-efficient attention (including PagedAttention)
so many concurrent requests can share limited hardware.

Using vLLM means the project would run (or manage) a model server instead of
only calling a hosted API such as OpenRouter or OpenAI.

## Why it comes up

Hosted APIs are simple and already power the documented Data 8 brains. Self-
hosted serving becomes interesting when the project wants open-weight models,
tighter control over data path and cost at volume, or research comparisons
that need identical serving conditions. vLLM is one common way to provide that
serving layer.

vLLM does not replace RAG, corpora, or tutoring prompts. It changes **how**
tokens are generated, not **what** course material the tutor can see.

## Advantages

- High throughput for concurrent student traffic on shared GPUs
- Efficient KV memory management for long prompts and many sessions
- Strong fit for open-weight models used in benchmarks or self-hosted demos
- Potential cost control at scale compared with per-token API pricing
- Reproducible serving stack for research comparisons

## Limitations

- Requires GPU capacity, deployment, monitoring, and upgrade work
- Operational burden the project does not have with OpenRouter alone
- Model quality and tutoring behavior still depend on weights and prompts
- Cold starts, scaling, and multi-tenant isolation need explicit design
- Less attractive while traffic and corpus experiments are still small

## When it is likely to help

vLLM is a better fit once the project is ready to **serve** models, not only
to **call** them: for example, a campus GPU host, a shared research cluster,
or a benchmark harness that must hit a local endpoint under load.

It is less compelling while the priority is corpus quality, pedagogical
evaluation, and interface experiments, all of which the current API-backed
setup already supports.

## Project stance

Keep hosted providers as the default path for day-to-day tutors. Treat vLLM as
an optional serving backend for open-weight or self-hosted experiments when
hardware and operations are available. Document any vLLM-backed brain the same
way other brains are documented: as a swappable model service behind the same
tutoring engine.
