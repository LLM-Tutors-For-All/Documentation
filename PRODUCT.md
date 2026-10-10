# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

LLM Tutors For All serves three audiences with equal priority:

- instructors and developers evaluating or deploying educational tutors;
- students learning how to access and use a tutor;
- researchers comparing language models and complete tutor systems.

## Product Purpose

The project documents practical, reproducible ways to build, deploy, use, and evaluate LLM-powered tutors. Success means that readers can understand available implementations, reproduce their setup, and judge tradeoffs in teaching quality, latency, reliability, and cost.

## Positioning

The project combines working tutor interfaces with a reproducible evaluation program. It treats deployments as both usable tools and research case studies, compares only implemented options, and publishes methodology and configuration alongside eventual results.

## Operating Context

The initial implementation is grounded in UC Berkeley Data 8 Spring 2026 course material. A shared retrieval-augmented tutoring engine is available through a local CLI, Discord, and Slack. Models are accessed through configurable model services, with OpenRouter currently documented as the default path.

## Capabilities and Constraints

- Documentation is built as a static MkDocs Material site.
- Course corpora, model brains, and tutor interfaces are documented separately so additional combinations can be added later.
- Benchmark results must not be presented until the evaluation design and judges are calibrated.
- Comparisons must be grounded in implemented, reproducible configurations rather than hypothetical claims.
- Setup documentation must remain usable on narrow screens and support light and dark color schemes.

## Brand Commitments

Preserve the LLM Tutors For All name, current logo, and the Berkeley-inspired navy-and-gold identity. The voice should remain factual, transparent about work in progress, and welcoming to technical and non-technical readers.

## Evidence on Hand

- Working interface screenshots and logos under `docs/assets/gallery/`.
- Tutor and setup diagrams under `docs/assets/`.
- Contributor portraits and social links under `docs/assets/contributors/` and `docs/assets/social/`.
- Current benchmark methodology and status in `docs/benchmark.md` and `docs/benchmark/evaluation.md`.
- No completed comparative benchmark results, testimonials, or outcome claims are currently available and none should be fabricated.

## Product Principles

1. Make complex tutor architecture understandable without hiding technical detail.
2. Help each audience quickly find the path relevant to them.
3. Separate measured evidence from plans and works in progress.
4. Keep deployment options modular and comparisons reproducible.
5. Treat accessibility and responsive behavior as requirements, not finishing touches.

## Accessibility & Inclusion

The documentation should meet WCAG 2.2 AA expectations, including keyboard access, visible focus, sufficient contrast, reduced-motion support, semantic structure, and readable layouts across mobile and desktop.
