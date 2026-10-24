---
hide:
  - navigation
  - toc
  - path
---

<section class="project-hero" markdown>

<div class="project-hero__copy" markdown>

# LLM Tutors For All

An applied research and discovery project exploring practical ways to deploy
LLM-powered tutors, with a focus on performance and cost tradeoffs across
services. We are developing reproducible benchmark harnesses to test tutor
models under consistent conditions.

<div class="project-hero__actions" markdown>
[Explore tutor options](tutor-options/index.md){ .md-button .md-button--primary }
[View benchmarks](benchmark.md){ .md-button }
</div>

</div>

</section>

<section class="project-details" markdown>

## Making LLM tutors easier to understand

There is no single best way to deploy an LLM tutor. The right approach depends
on where learners work, how quickly and reliably the tutor responds, and what
it costs to operate. LLM Tutors For All treats each implementation as both a
usable tutor and a research case study. The goal is to document working
deployment patterns and compare them through practical, repeatable benchmarks.

<div class="project-details__grid" markdown>

<div class="project-details__section" markdown>

### What we currently use

- **Course material:** the UC Berkeley Data 8 Spring 2026 corpus
- **Tutor design:** retrieval-augmented generation grounded in course content
- **Retrieval:** a local BM25 index, with optional provider-hosted embeddings
- **Model service:** OpenRouter, using `openai/gpt-4o-mini` by default and
  supporting other selectable models
- **Interfaces:** a local command-line tutor, Discord, and Slack
- **Persistent AIs:** a Grok Bot template and a Muse side-chat tutor

The self-hosted interfaces use one tutoring engine. Persistent AIs keep the
course corpus on a hosted cloud computer. Documenting both patterns lets the
project study how service and deployment choices affect latency, reliability,
usage, operating cost, and the learner experience.

</div>

<div class="project-details__section" markdown>

### Research direction

The current Data 8 GPT corpus and OpenRouter brain are the first framework
combination, not the intended limit of the project. Tutor interfaces and
framework components are documented separately so that future course corpora
and model brains can be added without restructuring the site.

Benchmark work will compare only options that have been implemented, rather
than assume that one approach is universally best. Results will include the
methodology, harness configuration, test questions, and measured data as
experiments are completed. This makes model comparisons repeatable instead of
depending on isolated demonstrations or impressions.

</div>

</div>

</section>
