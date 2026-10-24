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

<div class="benchmark-grid" markdown>

- Does the tutor identify the learner's mistake and locate it accurately?
- Does it provide correct, relevant, and actionable guidance?
- Does it guide the learner without revealing the final answer?
- Is its response coherent, natural, and appropriately encouraging?
- How much does each response cost, and how quickly is it produced?
- Do conclusions remain stable across repeated runs and different evaluators?

</div>

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

### Kinds of tutor systems

The project groups tutor systems into four types, from simplest to most
complex:

<div class="concept-list" markdown>

- **Model → text:** a language model answers on its own. Most existing
  benchmarks evaluate this case.
- **Model + corpus → text:** the model draws on course material, for example
  through retrieval-augmented generation (RAG).
- **Model + tooling = agent:** the model can call tools, for example through an
  MCP server or JupyterAI.
- **Model + tooling + many agents = agentic orchestration:** several agents
  work together, such as a supervisor agent that delegates to a coding agent
  and other specialized agents.

</div>

The team is planning how the harness will handle the more complex types:

- **RAG tutors:** embed each tutor's course corpus in a vector database, for
  example Firestore on Google Cloud.
- **Multi-agent tutors:** evaluate a supervisor agent together with the
  agents it coordinates.
- **Black-box tutors:** evaluate tutors whose internal context the harness
  cannot inspect, using only their responses.
- **Model routing:** test whether a router such as
  [Jev on OpenRouter](https://openrouter.ai/docs/guides/community/jev) can pick
  a suitable model for each question.

Cost is part of this comparison, including the tradeoff between cloud-hosted
agents and models run locally.

Research also suggests that benchmark results can vary with the language a
task is posed in. One idea under discussion is an ensemble that combines
judge votes given in different languages.

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

<div class="benchmark-grid benchmark-grid--outputs" markdown>

- pedagogical quality by evaluation dimension
- answer-leakage and response-length checks
- agreement between automated judges and human labels
- pairwise model preferences and judge consistency
- median and 95th-percentile latency
- token usage and estimated cost
- uncertainty intervals across repeated samples

</div>

Read [How evaluation works](benchmark/evaluation.md) for the scoring process,
reliability safeguards, and current development status.

## Project roadmap

The benchmark work is organized into five phases:

1. **Research related work:** review existing tutor benchmarks and evaluation
   methods.
2. **Build the benchmark and its infrastructure:** implement evaluation
   methods such as LLM-as-a-judge, paired comparison, simulated students,
   automated checks, and human ratings. *(In progress.)*
3. **Run evaluations:** compare models and tutor systems.
4. **Improve the benchmarks:** fix issues, add new areas to measure, and
   gather input, for example by surveying instructors.
5. **Share the work:** produce a poster and summary, and reach out to bring
   instructors on board.

## Related work

The project's research draws on work including:

- *Unifying AI Tutor Evaluation: An Evaluation Taxonomy for Pedagogical
  Ability Assessment of LLM-Powered AI Tutors*, which introduced MRBench
- *MathTutorBench: A Benchmark for Measuring Open-ended Pedagogical
  Capabilities of LLM Tutors*
- ELBench, whose method the team has reproduced on a small sample
- a four-score tutor benchmark from the University of Guangzhou covering
  General, Safety, Basic, and Cultivation skills
- studies of CS 61A's course bot and of LLM use in K–12 education
- Bloom's "2 sigma problem," on the gains from one-on-one tutoring

## Project resources

- [Benchmark repository](https://github.com/LLM-Tutors-For-All/benchmarks)
- [Inspect AI](https://inspect.aisi.org.uk/), the evaluation framework used by
  the project
- [Model options](model-options/index.md) currently documented on this site
- [NRP LLM API](https://datadisco.cdss.berkeley.edu/nrp-llm-api/), which
  provides access to models hosted on the National Research Platform
- [Quantization basics](https://ds-modules.github.io/Small_Models_SP26/quantizationbasics/),
  an introduction to running small models locally
