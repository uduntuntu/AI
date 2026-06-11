# Testing Methodology

Tests are executable behavioral specifications.

Prefer state-transition tests:

Before state
→ Input
→ After state
→ Observable output/effect
→ Invariant result

Failures should be attributable to one transition when practical.

Prefer deterministic integration tests for user-visible workflows.

Use unit tests for pure domain logic where they improve clarity.

Reusable invariants are preferred over duplicated assertions.

Coverage is a visibility tool, not the primary goal.

Do not change tests merely to make incorrect behavior pass. Diagnose the mismatch first.
