# Full-Stack Development Guide

A reusable guide for AI coding agents working across Flutter/Dart frontends and Firebase/TypeScript backends. Confirm every technology, version, path, and convention against the current repository before relying on it.

## How to start

- Inspect the repository, `git status`, and the nearest `AGENTS.md`, README, package manifests, and existing code before editing.
- Preserve unrelated user changes. Do not reset, overwrite, stage, commit, push, or deploy unless explicitly requested.
- Find the local owner of the behavior before making changes. Follow existing architecture, naming, state management, routing, and error handling.
- Keep changes small and focused. Do not infer missing product behavior; ask when a business or contract decision cannot be derived from code and docs.
- Use relevant local skills only when the task matches. Read their `SKILL.md` and check their advice against the repository's conventions.

## Frontend: Flutter and Dart

- Confirm the app structure and package choices before changing code.
- Prefer existing packages and patterns. For a new or unserved responsibility, possible defaults are `flutter_bloc` for state, `go_router` for routing, and `dio` for HTTP. These are suggestions, not permission to migrate or add dependencies.
- Ask before adding/changing dependencies, package choices, or architecture. Avoid duplicate packages with overlapping responsibilities.
- Keep widgets aligned with existing layout and accessibility patterns. For layout defects, inspect constraints and parent/child sizing before introducing fixed dimensions.
- Use declarative routing consistent with the existing router; preserve deep links, redirects, and navigation contracts.
- Use Dart pattern matching where it makes existing code clearer and consistent.
- For widget changes, use the focused widget-test workflow when the repository has tests. Do not introduce a broad testing framework for a localized task.
- Run the narrowest useful formatter, analyzer, or test command and report exactly what ran. Use Dart/Flutter MCP tooling if configured; setup is per developer machine and should not add repository-specific machine configuration.

Useful Flutter/Dart workflows include static analysis, pattern matching, focused widget tests, layout debugging, and declarative routing. Use a relevant local skill when available.

## Backend: Firebase, Firestore, and Stripe

This section applies when the repository uses these services. Verify runtime and framework versions first.

- Keep HTTP controllers responsible for methods, CORS, secret bindings, authentication, request validation, status codes, and response shape. Keep business rules and third-party workflows in domain modules.
- Centralize Firestore paths and access checks in the established database utilities; use the existing runtime configuration for Firebase and third-party clients.
- Treat exported function names, methods, request/response fields, error codes, webhook behavior, metadata, database shapes, and status strings as public contracts. Coordinate changes across callers and documentation.
- Verify payment webhook signatures against the raw request body. Preserve idempotency and make duplicate or delayed webhook delivery safe.
- Authenticate before authorizing. Derive identity from verified tokens, never caller-supplied identity or roles. Preserve the repository's role and resource ownership boundaries.
- Validate types, ranges, identifiers, and ownership at the request boundary. Use established error patterns and keep internal details out of client errors.
- Use database transactions for read-modify-write invariants and bounded batches for atomic groups. Design third-party/database sequences for retries and partial failure. Do not parallelize steps when ordering protects business invariants.
- Preserve idempotency keys, resource ownership checks, schedule ordering, quantities, and local time-zone semantics where applicable.
- Database security rules may not protect privileged server-side writes; enforce authorization in server code at each write boundary.
- Use structured logging. Never log tokens, secrets, passwords, raw payment data, verification links, or unnecessary personal information.
- Do not edit generated output. Do not expose or commit `.env` values. Treat example environment files as potentially incomplete; consult runtime configuration for required variable names, never secret values.
- Never deploy unless explicitly asked. Do not run production writes, backfills, recursive deletes, or data imports/exports without authorization, bounded targets, validation, and rollback planning.

For payment or subscription changes, read the repository's flow documentation. For database shape or status changes, read its schema documentation. Consult any project map before broad searches when available. Update relevant references whenever documented flows or schemas change.

## Review and delegation

- Complete routine, localized work directly. Delegate only medium, large, risky, or unclear work when a bounded specialist review materially improves correctness or delivery time.
- For payment, subscription, authentication, secrets, or sensitive-data changes, use a security/privacy review. For medium or larger backend changes, review the actual diff plus nearby callers, contracts, and tests.
- Reviews should examine end-to-end state transitions, authorization, idempotency, ownership, ordering, partial failure, concurrency, money/tax, time-zone behavior, and privacy when relevant.
- Keep delegated work scoped to clear questions or file ownership. The primary agent owns integration and final decisions.

## Verification and handoff

- Use the repository's existing scripts and narrowest relevant checks. Report commands, results, and skipped checks. Do not claim tests or coverage that do not exist.
- Before finishing, inspect the diff and status; confirm the requested behavior, connected contracts/docs, and scope. Do not stage or commit unless requested.
- Summarize changed files, verification results, and any remaining risk or decision clearly.

## Skill upkeep

Treat vendored skills as maintained dependencies. Review skill diffs and security flags before relying on updates; refresh them separately from application changes. Review skills periodically and before major framework upgrades. Do not copy generic rules that conflict with the actual app architecture.
