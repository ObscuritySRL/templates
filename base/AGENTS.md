# AGENTS

Blunt rules. Keep it fast. Keep it tidy. No fluff.

## Scope

Applies to entire repo.

## TL;DR

- Plan before implementing. Understand the problem and existing code first.
- Default to Bun. Do not assume Node unless repo says so.
- Performance first in measured hot paths. Prefer fewer allocations when profiled.
- No helpers unless explicitly requested.
- No abbreviations. Never rename user-provided identifiers.
- Alphabetize anything unordered. Do not reorder when order matters.
- Minimal, surgical diffs. Do not "clean up" unrelated code.
- Run tests after changes. Do not submit broken code.

## Style

- Language: mirror the repo.
- Formatting: respect repo config (Prettier, ESLint, etc.). Honor inline ignores.
- Sort: imports/exports/objects/enums/type members alphabetically when order is not critical.
- Strings: follow repo convention. Use numeric separators when helpful.
- Comments: terse, value-add only. Prefer compact JSDoc over inline chatter.

## Public API

- Respect current export shape and entry points. Do not change public API without explicit request.
- When adding API:
  - Provide precise TypeScript typings and overloads as needed.
  - Keep names stable and descriptive. Do not break existing signatures or semantics.
  - Document with one short runnable example.

## Performance

Performance is critical. Profile first; optimize proven hot paths. Avoid cleverness without numbers.

- Reuse Buffer/TypedArray/DataView instances in hot paths.
- Avoid implicit copies, JSON roundtrips, and large-array spreads in loops.
- Tight loops; hoist constants; avoid closures in hot paths.
- Prefer `Buffer.allocUnsafe` where safe; validate boundaries once.
- Never expose uninitialized memory. If data may be observed outside the function (returned, logged, thrown, shared), use zero-filled alloc or explicitly fill.
- Minimize allocations. Pool objects when appropriate.
- Prefer iteration over collection creation (avoid intermediate arrays).
- Use bitwise only when it reduces work and stays correct (32-bit limits; signedness; readability cost).

## Errors

- Use existing error types in the repo. Keep messages concise and actionable.
- Do not swallow errors. Surface root cause; no apology prose.

## Docs

- Compact JSDoc with a single, runnable example.
- README examples: short and performance-minded. Prefer reuse over allocation.

## Testing

- Run tests after every change. Do not leave the codebase in a broken state.
- Use `bun` scripts. Do not add Node-only tooling.
- Keep examples under `example/` (or existing examples directory). Avoid adding dependencies.
- Remove temporary benchmarks/diagnostics before finishing.

## Benchmarking

- Benchmark when comparing approaches or making performance claims.
- Use `bun` for benchmarks. Measure multiple iterations; report median/p99.
- Compare against the existing implementation, not just in isolation.
- Include memory allocation metrics when relevant.
- Do not claim "faster" without numbers.

## Commits

Follow conventional commits:

```
type(scope): description
```

- `type`: what kind of change (feat, fix, refactor, docs, test, chore, perf, etc.)
- `scope`: optional, affected area in parentheses
- `description`: lowercase, imperative, no period

Examples:
- `feat(auth): add token refresh`
- `fix: resolve memory leak in parser`
- `perf(cache): reduce allocations in hot path`

## Do Not

- Do not add helpers/utilities unless explicitly requested.
- Do not assume the user knows best. Suggest better approaches that fit this configuration.
- Do not reformat broadly. Change only what you touch.
- Do not add licenses/headers or new linters/tooling.
- Do not broaden platform support or add polyfills without request.
- Do not guess or fabricate information. Failure is acceptable; incorrect information is not. Say "I don't know" when uncertain.

## Conventions

- Sort when order is not critical: attributes, class names, enum members, exports, function calls, imports, map/set initializers, object keys, switch cases, type fields, union members.
- Naming: descriptive, full words. No shorthands (e.g., `address`, not `addr`).
- Keep alignment/one-liners consistent with existing code.
- Prefer explicit `void` when deliberately discarding a value.

Stick to this. Ship small, surgical, fast changes.
