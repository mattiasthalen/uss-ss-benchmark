<!--
Sync Impact Report:
- Version change: 1.0.0 → 1.1.0
- Modified principles: None
- Added sections: None
- Removed sections: None
- Templates requiring updates:
  - ✅ updated: .specify/templates/plan-template.md
  - ⚠ pending: .specify/templates/commands/*.md (directory missing)
- Follow-up TODOs:
  - TODO(RATIFICATION_DATE): original adoption date unknown
-->
# USS-SS Benchmark Constitution

## Core Principles

### I. Reproducible Benchmarks
- Benchmark runs MUST be deterministic given identical inputs, seeds, and versions.
- Dependencies, data versions, and configuration MUST be pinned and recorded.
- Hardware and OS details MUST be captured with each published result.
Rationale: Results that cannot be reproduced are not actionable for comparison.

### II. Faithful Workloads
- Benchmarks MUST represent real USS/SS workloads, not synthetic micro-cases that
  change semantics.
- Any simplification MUST be documented and justified in the benchmark spec.
Rationale: Fidelity protects against optimizing the wrong problem.

### III. Measurement Integrity
- Every benchmark MUST define a measurement protocol: warmup, sample count,
  timing source, and aggregation method.
- Results MUST report variance or distribution, not single best runs.
- Cherry-picking runs or configurations is prohibited.
Rationale: Integrity demands comparable, statistically honest measurements.

### IV. Correctness Before Performance
- Functional correctness MUST be validated before performance claims.
- Performance changes MUST include before/after evidence and link to the tests
  that validate behavior.
Rationale: Fast but wrong results are regressions, not improvements.

### V. Simplicity and Traceability
- Prefer the simplest design that meets the benchmark requirement.
- Every benchmark result MUST be traceable to a specific code version, dataset,
  and command.
Rationale: Simplicity reduces hidden variables; traceability supports auditing.

### VI. Functional Composition
- Prefer many small, single-purpose, mostly pure functions over large
  multi-responsibility functions.
- Side effects and shared mutable state MUST be minimized and isolated.
- Data flow MUST be explicit, and function composition preferred when possible.
Rationale: Functional decomposition improves testability and reduces hidden state.

## Benchmarking Standards

- Each benchmark MUST include a spec describing inputs, expected outputs, and
  termination conditions.
- Datasets MUST be versioned, checksummed, and retrievable via documented steps.
- Baselines MUST be captured before material changes and retained for comparison.
- Measurement artifacts (logs, configs, summaries) MUST be stored in the repo or
  linked from an immutable storage location.

## Development Workflow

- All work MUST start with a feature spec and implementation plan using the
  repository templates.
- Changes affecting benchmarks MUST update the measurement protocol and baseline
  notes in the relevant spec.
- Reviews MUST verify compliance with the Core Principles and this section.

## Governance
- This constitution supersedes local conventions and templates if conflicts arise.
- Amendments require a documented rationale, an impact summary, and team approval.
- Versioning follows semantic versioning:
  - MAJOR for breaking governance changes or principle removals.
  - MINOR for new principles or materially expanded guidance.
  - PATCH for clarifications and non-semantic edits.
- Compliance is reviewed in every plan and PR by checking the Constitution Check
  section in planning docs.

**Version**: 1.1.0 | **Ratified**: TODO(RATIFICATION_DATE): original adoption date unknown | **Last Amended**: 2025-12-31
