# TypeScript Review

## Prefer strong types; avoid type inspection on known types
The reviewer MUST:
- Avoid runtime type inspection (`typeof`, `instanceof`) when the type is known or enforced by TypeScript.
- Restrict runtime checks to untyped inputs or boundary validation (e.g., API payloads).

Discouraged:
```ts
function labelCount(count: number) {
  if (typeof count === "number") return `${count} items`;
  return "n/a";
}
```

## Avoid `any` and `unknown` when possible
The reviewer MUST:
- Reject `any` unless it is a last-resort boundary with clear justification.
- Require immediate narrowing of `unknown` with explicit type guards.

The reviewer SHOULD:
- Prefer generics, `satisfies`, and well-scoped interfaces over `any`.

## Type casting must be justified
The reviewer MUST:
- Require a comment or invariant when using `as`, non-null assertions (`!`), or unsafe casts.
- Prefer `satisfies` or type guards before asserting a type.

Acceptable with proof:
```ts
const payload = parse(input) as Payload; // validated by parse schema
```
