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

- **Mistake identification:** Did the tutor recognize an error?
- **Mistake location:** Did it accurately point to where the error occurred?
- **Answer revealing:** Did it avoid giving away the final answer?
- **Guidance:** Did it provide correct and relevant help?
- **Actionability:** Is the learner's next step clear?
- **Coherence:** Does the response fit the preceding conversation?
- **Tone:** Is the response encouraging, neutral, or offensive?
- **Human-likeness:** Does the response sound natural rather than robotic?

The categorical labels and their distributions remain part of the report.
Numeric summaries are useful for comparison, but they do not replace the
underlying rubric.

## More than one kind of evaluator

No single automated judge is assumed to be correct. The platform supports
several complementary approaches:

- **Rubric judging** scores one response across the pedagogical dimensions.
- **Cross-provider juries** combine judges from different model vendors.
- **Pairwise judging** compares two responses in both presentation orders.
- **Human ratings** provide an external reference for automated judges.
- **Calibration datasets** test judges against existing expert labels from
  MRBench and the BEA 2025 shared task.

Judge quality is measured with agreement statistics such as Cohen's kappa, not
only raw agreement. Pairwise comparisons swap response order to expose position
bias, and self-judging experiments check whether a model favors responses from
its own provider.

## Reliability and fair comparison

The methodology includes safeguards intended to prevent a clean-looking
leaderboard from hiding unstable results:

- run each item multiple times and retain raw responses
- pin model versions and record generation settings where providers allow it
- keep reference answers away from the tutor while making them available to
  evaluators
- report answer leakage separately from general response quality
- use clustered bootstrap confidence intervals for repeated conversations
- report latency separately as median and 95th percentile
- publish judge parsing failures, pairwise inconsistencies, and excluded runs

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

!!! note "How to interpret this section"
    Until result pages are published, descriptions here explain what the
    framework is designed to measure. They should not be read as claims that
    one model or tutor has already outperformed another.

[Return to the benchmark overview](../benchmark.md)
