# JavaScript Review

TypeScript-specific typing rules are in `review/typescript.md`.

## Prefer functional over OO
The reviewer SHOULD:
- Prefer pure functions and data transforms over classes when state is not required.
- Encourage small, composable utilities instead of deep inheritance trees.

The reviewer MUST:
- Flag new classes that only wrap stateless helpers or act as namespaces.

Acceptable:
```js
const formatUser = (user) => `${user.firstName} ${user.lastName}`;
```

Discouraged:
```js
class UserFormatter {
  format(user) {
    return `${user.firstName} ${user.lastName}`;
  }
}
```

## Use `switch` for enum-like values
The reviewer MUST:
- Flag `if/else if` chains that branch on the same enum-like value when a `switch` is clearer.

Preferred:
```ts
switch (status) {
  case "idle":
    return renderIdle();
  case "running":
    return renderRunning();
  case "failed":
    return renderFailed();
  default:
    return assertNever(status);
}
```

Discouraged:
```ts
if (status === "idle") return renderIdle();
if (status === "running") return renderRunning();
if (status === "failed") return renderFailed();
```

## Avoid duplicated code
The reviewer MUST:
- Flag duplicated logic and suggest extracting helpers or shared utilities.

The reviewer SHOULD:
- Prefer a single source of truth for calculations and formatting.

## Use modern JavaScript APIs when available
The reviewer SHOULD:
- Prefer modern APIs like `Object.hasOwn`, `Array.prototype.at`, `flatMap`, `replaceAll`, `URL`, `AbortController`, and `Promise.any` when they improve clarity.
- Confirm runtime targets or polyfills before requiring newer APIs.
