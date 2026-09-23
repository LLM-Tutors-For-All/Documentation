# Benchmarking LLM tutors

Choosing an educational model requires more than checking whether it can
produce the right final answer. A useful tutor should recognize where a learner
went wrong, offer an appropriate next step, avoid doing the work for them, and
remain practical to deploy.

LLM Tutors For All is building a reproducible benchmark for comparing both
**language models** and, later, complete **tutor systems** under consistent
conditions. The goal is to help instructors and developers understand the
tradeoffs among teaching quality, cost, speed, and deployment constraints.

!!! info "Work in progress"
    The benchmark platform is under active development. This section describes
    the current scope and methodology; comparative results and recommendations
    will be published after the evaluation design and judges have been
    calibrated.

## What the benchmark asks

The project studies questions such as:

- Does the tutor identify the learner's mistake and locate it accurately?
- Does it provide correct, relevant, and actionable guidance?
- Does it guide the learner without revealing the final answer?
- Is its response coherent, natural, and appropriately encouraging?
- How much does each response cost, and how quickly is it produced?
- Do conclusions remain stable across repeated runs and different evaluators?

These questions are evaluated separately. A model that is inexpensive or fast
may not be the strongest pedagogical choice, while a high-quality response may
be impractical at scale. The benchmark will report these tradeoffs rather than
collapse them into a single "best model" score.

## What is being compared

### Models

The initial work compares proprietary and open-weight language models accessed
through a common evaluation harness. This includes models served by commercial
APIs as well as models available through shared or self-hosted infrastructure.
Each model receives the same tasks and tutoring instructions.

### Tutor systems

A tutor is more than its underlying model. System prompts, retrieval, course
context, guardrails, and orchestration can all change the learner experience.
The platform includes a common adapter design so complete tutor systems can
eventually be tested with the same tasks and scoring methods as raw models.

### Interactive settings

The project is also preparing evaluations with simulated students, including
multi-turn tutoring and office-hours-style queues. This work will examine
answer leakage, responsiveness, attention allocation, wait time, and
starvation. Simulation results will only be used after the simulated students
pass explicit validity checks.

## What a benchmark run produces

For each task, the harness records the full prompt and response, model and
configuration, token use, timing, and scoring details. Responses can then be
rescored without generating them again.

Reports are designed to include:

- pedagogical quality by evaluation dimension
- answer-leakage and response-length checks
- agreement between automated judges and human labels
- pairwise model preferences and judge consistency
- median and 95th-percentile latency
- token usage and estimated cost
- uncertainty intervals across repeated samples

Read [How evaluation works](benchmark/evaluation.md) for the scoring process,
reliability safeguards, and current development status.

## Project resources

- [Benchmark repository](https://github.com/LLM-Tutors-For-All/benchmarks)
- [Inspect AI](https://inspect.aisi.org.uk/), the evaluation framework used by
  the project
- [Model options](model-options/index.md) currently documented on this site
