# Testing Methodology

Tests are executable behavioral specifications.

Prefer state‑transition tests:

Before state
→ Input (must invoke a reachable entry point)
→ After state
→ Observable output/effect (return value, state change, log, file, UI, etc.)
→ Invariant result

Failures should be attributable to a single transition (the step under test) whenever practical.

Prefer deterministic integration tests for user‑visible workflows – mock or fix any source of nondeterminism (time, random IDs, external services) so the same input always yields the same observable effect.

Use unit tests for pure domain logic where they improve clarity.

Use reusable fixtures (initial snapshots, mocked services, sample data) to avoid duplicated setup code across tests.

Reusable invariants are preferred over duplicated assertions.

**Reachable‑code requirement** – a test must invoke code that is reachable from the normal entry points of the application (CLI commands, public API functions, published classes, etc.). If the targeted code is never executed in a running build, the test
must be marked invalid and not added.

**No placeholder‑pass tests** – do not create a test whose only assertion is `assert True` (or any trivially true condition) unless the test also executes a reachable piece of production code. Every test must contain at least one observable assertion that
depends on the execution of the code under test.

**Outcome‑driven tests** – write the test so that its assertion describes the final Runtime snapshot after the feature is applied.
1. Capture the initial snapshot.
2. Call the public entry point the user will actually use.
3. Define the *expected* snapshot (desired final values).
4. Assert `actual_snapshot == expected_snapshot` (or that all invariants on the actual snapshot hold).
5. Do not add intermediate step‑by‑step assertions; the test must fail until the implementation produces the exact final state.

**Fail‑first** – when generating an outcome‑driven test, first verify that the current implementation does **not** satisfy the expected snapshot. If it already does, adjust the expectation so the test initially fails, then let the user drive the
implementation to pass.

Do not change tests merely to make incorrect behavior pass. Diagnose the mismatch first.

Coverage is a visibility tool, not the primary goal.

*In short: write deterministic, reachable tests that assert the final desired state of the system; let them fail first and only then implement the feature that makes them green.*