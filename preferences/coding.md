# Coding preferences

- **Prefer idiomatic, language‑specific design** – write code the way the language community expects it, using conventional patterns and naming styles.
- **Apply type hints at public‑API boundaries** – every function, method, or class that is part of a module’s public surface should have type annotations for its parameters and return value. Internal helpers may omit them when they add noise.
- **Favor small, single‑purpose modules** – each file should own a clear responsibility and expose a minimal public interface.
- **Avoid premature abstraction** – introduce abstractions (e.g., base classes, utilities) only when a concrete need is visible in at least two places.
- **Prefer the standard library or well‑established third‑party packages** – reach for external dependencies only after confirming the feature is not already available natively.
- **Separate core domain logic from I/O and presentation** – keep business rules in pure, framework‑agnostic objects; any file access, console output, UI rendering, or network communication should be performed by thin façade functions that depend on the domain layer, not the other way around.
- **Use immutable domain objects when their state is stable after loading** – `dataclasses(frozen=True)`, `namedtuple`, or simple value objects help prevent accidental mutation.
- **Never embed secrets in prompts, source files, markdown, or test code** – if a secret is required, ask the user for the location of a read‑only `.env` file (or similar).
    - *Only the variable name may be mentioned; never echo its value.*
    - The assistant must treat `.env` as an external, immutable resource.
- **Prefer `python‑dotenv` (or equivalent) for loading environment variables** – if a required variable is missing, request the user to add it to the `.env` file rather than hard‑coding defaults.
- **Keep conversational context minimal** – do **not** propose code diffs, implementation snippets, or open files unless the user explicitly requests them. Acknowledge the existence of a file and offer to view it later, but wait for a clear request before calling `view_file`.
- **Use `snake_case` for identifiers** – follow PEP 8 naming conventions throughout the codebase.
- **Ask before running any destructive command** – this includes file‑system changes **and** version‑control operations.
      For VCS actions (e.g., `git commit`, `git push`):
      1. **If a commit is to be created**, ask the user to **review and confirm the commit message**.
      2. **If a push (or any remote update) is requested**, ask the user **whether the push is explicitly allowed**.
      After the user gives a single “yes” response that covers both items, perform the VCS command(s) without an additional generic confirmation prompt.