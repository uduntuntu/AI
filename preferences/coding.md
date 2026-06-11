# Coding Preferences

- Prefer idiomatic language-specific design.
- Use type hints at public/module boundaries where practical.
- Prefer small modules with clear responsibilities.
- Avoid premature abstraction.
- Use standard library or well-established packages before custom machinery.
- Keep domain logic separate from I/O and presentation.
- Use immutable domain objects when the data is stable after loading.
- Do not store secrets in prompts, code, markdown, or tests.
- Do not run destructive commands without explicit confirmation.
