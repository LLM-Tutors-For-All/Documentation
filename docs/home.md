---
hide:
  - navigation
  - toc
  - path
---

<section class="project-hero" markdown>

# LLM Tutors For All

An applied research and discovery project exploring practical ways to deploy
LLM-powered tutors, with a focus on performance and cost tradeoffs across
services.

[Explore tutor options](options.md){ .md-button .md-button--primary }
[View benchmarks](benchmark.md){ .md-button }

</section>

<section class="project-details" markdown>

## Making LLM tutors easier to understand

There is no single best way to deploy an LLM tutor. The right approach depends
on where learners work, how quickly and reliably the tutor responds, and what
it costs to operate. LLM Tutors For All treats each implementation as both a
usable tutor and a research case study. The goal is to document working
deployment patterns and compare them through practical, repeatable benchmarks.

### What we currently use

- **Course material:** the UC Berkeley Data 8 Spring 2026 corpus
- **Tutor design:** retrieval-augmented generation grounded in course content
- **Retrieval:** a local BM25 index, with optional OpenAI embeddings
- **Model service:** an OpenAI-compatible API using `gpt-4o-mini` by default
- **Interfaces:** a local command-line tutor, Discord, and Slack

Using one tutoring engine across these interfaces lets the project study how
the surrounding service and deployment choice affects latency, reliability,
API usage, operating cost, and the learner experience.

### Research direction

The current Data 8 GPT corpus and OpenAI-compatible brain are the first
framework combination, not the intended limit of the project. Tutor interfaces
and framework components are documented separately so that future course
corpora and model brains can be added without restructuring the site.

Benchmark work will compare only options that have been implemented, rather
than assume that one approach is universally best. Results will include the
methodology and measured data as experiments are completed.

## Project contributors

<div class="contributors" markdown>

- **Benjamin Telanoff**
- **Edwin Vargas Navarro**
- **Silas Santini**

</div>

[View the project source and contributors](https://github.com/LLM-Tutors-For-All/LLM-Tutors-For-All)

</section>
