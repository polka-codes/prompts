# Polkadot SDK Review

## Storage and bounded data
The reviewer MUST:
- Look for storage that can grow with user input (unbounded `Vec`, maps without limits or cleanup).

The reviewer SHOULD:
- Recommend bounded collections (e.g. `BoundedVec`) or explicit cleanup/garbage collection.
- Ensure hooks or extrinsics that process storage have bounded work per block.

## Access control and origins
The reviewer MUST:
- For each `#[pallet::call]`, ensure the origin is validated (`ensure_signed`, `ensure_root`, or a custom origin).
- Confirm permission checks match the sensitivity of the action (e.g. config changes should be `Root` or a privileged origin, not arbitrary signed users).

The reviewer SHOULD:
- Prefer explicit origins (e.g. `AdminOrigin`, `UpdateConfigOrigin`) over blanket `ensure_root` unless absolutely necessary.

## Events and errors
The reviewer SHOULD:
- Ensure important state changes emit events with clear payloads that describe the transition (start/stop, created/closed, funds moved, etc.).
- Use `#[pallet::error]` variants instead of ad-hoc strings or panics.

## Hooks and migrations
For `on_initialize`, `on_finalize`, `on_runtime_upgrade`, etc., the reviewer MUST:
- Check per-block work is bounded and weight-aware.
- Ensure migrations are versioned and idempotent.

The reviewer SHOULD:
- Ask for tests or clear documentation for migrations.
