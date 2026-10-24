# How evaluation works

The benchmark separates response generation from scoring. This makes model
comparisons repeatable and allows new scoring methods to be applied to existing
responses without paying to generate them again.

## Evaluation pipeline

1. **Build representative tasks.** Items contain the conversation so far, the
   educational problem, a private reference answer or solution, and any
   item-specific rubric.
2. **Generate tutor responses.** Candidate models receive the same task and
   tutoring prompt. Multiple samples are collected because hosted models are
   not perfectly deterministic.
3. **Run inexpensive checks.** Automated checks measure properties such as
   response length and possible answer leakage.
4. **Score teaching quality.** Calibrated LLM judges evaluate each response
   against a pedagogical rubric. Pairwise judging can also compare two
   responses directly.
5. **Analyze the run.** Reports combine quality scores with token use, estimated
   cost, latency, sample counts, and uncertainty intervals.

The complete prompts, responses, settings, usage, and timing are retained in
the evaluation logs so that published numbers can be traced back to their
source.

## Pedagogical dimensions

The initial rubric follows the eight dimensions used by
[MRBench](https://aclanthology.org/2025.naacl-long.57/):

<div class="benchmark-grid benchmark-grid--dimensions" markdown>

- **Mistake identification:** Did the tutor recognize an error?
- **Mistake location:** Did it accurately point to where the error occurred?
- **Answer revealing:** Did it avoid giving away the final answer?
- **Guidance:** Did it provide correct and relevant help?
- **Actionability:** Is the learner's next step clear?
- **Coherence:** Does the response fit the preceding conversation?
- **Tone:** Is the response encouraging, neutral, or offensive?
- **Human-likeness:** Does the response sound natural rather than robotic?

</div>

The categorical labels and their distributions remain part of the report.
Numeric summaries are useful for comparison, but they do not replace the
underlying rubric.

## More than one kind of evaluator

No single automated judge is assumed to be correct. The platform supports
several complementary approaches:

<div class="method-list" markdown>

- **Rubric judging** scores one response across the pedagogical dimensions.
- **Cross-provider juries** combine judges from different model vendors.
- **Pairwise judging** compares two responses in both presentation orders.
- **Human ratings** provide an external reference for automated judges.
- **Calibration datasets** test judges against existing expert labels from
  MRBench and the BEA 2025 shared task.

</div>

Judge quality is measured with agreement statistics such as Cohen's kappa, not
only raw agreement. Pairwise comparisons swap response order to expose position
bias, and self-judging experiments check whether a model favors responses from
its own provider.

## Evaluator methods in development

Each judging approach has a team member leading its research and
implementation. The notes below describe what has been built so far and what
early pilot runs have shown. They are working observations from small samples,
not benchmark results.

### Single-output judging

*Lead: Lindsay Lai*

A judge sees one response at a time and scores it against the rubric. To avoid
the ties and coarse distinctions of integer scales such as 1–10, the judge
uses continuous, probability-weighted scores and a multi-dimensional rubric.
A leaderboard and a set of judge diagnostics compare tutors and check how the
judge itself behaves:

- **Ceiling rate:** how often the judge gives the top label. A high rate means
  the judge is not separating responses well.
- **Length correlation (`length_rho`):** a value above zero means the judge
  rewards longer answers.

In early runs, the judge favored longer answers and gave very high scores to
most responses, which made it hard to tell tutors apart. Addressing these
issues is part of judge calibration.

### Pairwise comparison

*Lead: Khas-Erdene Tsogtsaikhan*

A person or an LLM sees two responses to the same prompt and picks the better
one, using a clearly defined rubric covering qualities such as completeness and
clarity. Forcing a choice avoids the arbitrariness of assigning a 1–10 score
and requires the evaluator to reason about the differences. Each pair is
judged in both presentation orders.

### LLM as a jury

*Lead: Justin Le*

Several LLM jurors run pairwise comparisons on tutor responses. Instead of
simply counting wins, the jury uses a modified Bradley–Terry model:

```text
P(A > B) = σ((S_A − S_B) / σ_k)
```

Here, `S_A` and `S_B` are the overall strengths of the two tutors, `σ` is the
logistic function, and `σ_k` is a reliability parameter for juror `k`. A lower
`σ_k` means
the juror's votes agree more closely with the global ranking. The
implementation reads the jurors' comparison logs and returns an overall score
for each tutor and a reliability estimate for each juror. In the source
paper, this approach outperformed the standard Bradley–Terry model on
benchmark datasets.

For error classification, where jurors label responses by error severity
(minor, neutral, major, or critical), the team is exploring logistic
regression to combine juror votes. Each juror would get a learned weight
reflecting its reliability, trained on human-labeled examples.

### Self-judging

*Lead: Yiran Hu*

Research suggests that models can prefer their own answers, although a model
that rates itself highly may simply be better. To tell these apart, the
self-judge benchmark has each model judge the tutor responses it wrote
alongside outside judges that wrote none of them. The `ltb self-judge` command
supports two modes:

- **pairwise:** pick the better of two responses (A, B, or tie), asked in both
  orders
- **rubric:** label one response on the eight MRBench dimensions

The output is a **self-preference score** for each model: how the model rates
its own answers minus how the outside judges rate them. A score of 0 means the
model judges itself fairly; a positive score means it favors itself.

In an early pilot with three models, gpt-oss favored its own responses against
both other models while Kimi did not. On the MRBench items, the pilot showed no
evidence of extreme self-preference.

### Reproducing published benchmarks

*Lead: Christopher Mach*

The team has reimplemented the ELBench paper's method and run it on a small
sample dataset to reproduce the paper's metrics. A larger dataset is needed
before drawing conclusions. The team also reviewed a four-score benchmark from
the University of Guangzhou (General, Safety, Basic, and Cultivation). In that
benchmark, the tested models scored well on every category except
Cultivation, which asks whether a response reflects the intuition of a domain
expert.

### Classifying student questions

Before choosing how to respond, a tutor may need to recognize what kind of
help a student is asking for. The team tested 20 models as question-type
classifiers. Each one sorted a student message into one of five categories:
debugging, conceptual, hint, remediation, or other. Every model saw the 26
pilot items with the options shuffled into three different orders, and the
answers were scored against hand labels.

Accuracy was similar across all models. Decision models such as Jev, Liquid,
and Perplexity were 10 to 50 times faster and also report a confidence score.
More labeled examples are needed before choosing a classifier.

## Reliability and fair comparison

The methodology includes safeguards intended to prevent a clean-looking
leaderboard from hiding unstable results:

<div class="method-list" markdown>

- run each item multiple times and retain raw responses
- pin model versions and record generation settings where providers allow it
- keep reference answers away from the tutor while making them available to
  evaluators
- report answer leakage separately from general response quality
- use clustered bootstrap confidence intervals for repeated conversations
- report latency separately as median and 95th percentile
- publish judge parsing failures, pairwise inconsistencies, and excluded runs

</div>

Latency reflects a service at a particular time, not only the model itself.
Likewise, automated pedagogical scores are meaningful only when the judge has
shown adequate agreement with human labels.

## Current status

As of September 2026, the baseline evaluation platform can generate and cache
responses, run rubric and pairwise scoring, calibrate judges, and report
quality, cost, and latency. The first pilot uses Data 8 dialogue tasks.

The team is currently calibrating judges and expanding the pilot dataset before
publishing model comparisons. Human-rating, simulated-student, office-hours
queue, and complete tutor-adapter evaluations are planned work rather than
finished results.

### October 2026 update

Each LLM-as-a-judge method now has a working implementation and is being
tested on pilot data (see
[Evaluator methods in development](#evaluator-methods-in-development)). The team
is also planning how the harness will evaluate tutors that are more than a
single model, such as tutors that search a course corpus or run as agents. See
[Kinds of tutor systems](../benchmark.md#kinds-of-tutor-systems).

!!! note "How to interpret this section"
    Until result pages are published, descriptions here explain what the
    framework is designed to measure. They should not be read as claims that
    one model or tutor has already outperformed another.

[Return to the benchmark overview](../benchmark.md)
