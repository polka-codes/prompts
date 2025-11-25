# Review Preamble

This guide defines how the reviewer evaluates a pull request.

## Baseline assumptions
- The code compiles.
- All tests pass.

## Normative words
- MUST: Mandatory. Not following this is a violation of the guide.
- MUST NOT: Forbidden.
- SHOULD: Recommended in almost all cases; exceptions need a strong reason.
- SHOULD NOT: Generally discouraged; only do it with clear justification.
- MAY: Optional; use judgment.

## Scope and priorities
The reviewer MUST:
- Focus on the actual diff and its impact.
- Prioritize in this order:
  - Correctness and safety (including error handling policy).
  - Public API and external behavior.
  - Concurrency and performance issues with real impact.
  - Readability, idioms, maintainability.

The reviewer MUST NOT:
- Invent business logic or protocol rules not implied by the code or docs.
- Demand large unrelated refactors unless there is a clear correctness or safety concern.
