---
name: clean-code
description: Write backend and frontend code that is plain, readable and easy to maintain or scale. No AI slop, no over-engineering. Use on any task that writes or changes app code (API, services, database, UI components, scripts), and when the user says "clean code", "no slop", "keep it simple" or "easy to maintain".
---

# Clean Code

Write code a tired teammate can read at 2am and change safely. Plain beats clever. Plain beats "professional".

## Before writing

1. Read the existing code. Copy its folder layout, naming, error style and libraries. Do not bring your own style.
2. Use what is already there (helper, component, library) before writing new code.
3. Do only what was asked. Name anything you left out in one line.

## Naming and shape

- Names say what a thing is or does: `getUnpaidInvoices`, not `handleData`, `processItems`, `utils`, `helper`, `manager`.
- One function does one job. If you need "and" to describe it, split it.
- Max about 40 lines per function and about 3 levels of nesting. Use early returns instead of deep `if`.
- Pure logic (calculations, rules) lives apart from I/O (database, HTTP, files). Pure parts are easy to test and reuse.
- No magic numbers or strings. Give them a named constant when used twice or when the meaning is not obvious.

## Do not add (this is the slop and the "too professional")

- Abstraction used once: interface with one implementation, factory, wrapper class, base class "for later".
- Options, config flags or generic parameters nobody asked for.
- Comments that repeat the code (`// increment i`). Comment only the why, in one line.
- Long docstrings on obvious functions. Emoji or decorative text in code, logs or commits.
- `try/catch` that swallows the error or just logs and continues. Catch only what you can handle; let the rest bubble up to one central handler.
- Checks for cases that cannot happen. Validate at the edges only (request body, env vars, external API response).
- Copy-paste blocks. Third copy = extract. Two copies are fine.
- New dependency for a few lines of code.

## Backend

- Layers stay thin and in one direction: route/controller (parse and respond) -> service (business rules) -> data access (queries). No SQL in routes. No HTTP objects in services.
- Validate input once at the route. Return clear status codes and one consistent error shape.
- Config and secrets come from environment variables, never hardcoded.
- Scaling basics from day one: pagination on list endpoints, indexes on columns you filter by, no query inside a loop (N+1), no global mutable state, idempotent writes where a retry is possible.
- Migrations for every schema change. Never edit the database by hand.

## Frontend

- Small components, one job each. Group files by feature (`features/cart/...`), not by type (`all-components/`).
- Keep state as local as possible. Lift it up only when two components need it. Do not add a global store for one screen.
- Fetch data in one place per feature (hook or loader). Components only show data.
- Show loading, empty and error states. Not just the happy path.
- Accessibility is not optional: real `button` and `a` elements, labels on inputs, alt text.
- Do not memoize, debounce or virtualize until it is actually slow.

## Finish

- Run the formatter and linter the project already uses.
- New non-trivial logic gets one small test. Trivial changes need none.
- A shortcut with a known limit gets one comment: `shortcut: <limit>, <when to upgrade>`.
- End the reply with 1-2 lines: what you skipped or did not check, and any risk.
