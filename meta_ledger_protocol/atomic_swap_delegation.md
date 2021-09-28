# Atomic Swap Delegation Meta Ledger Protocol

## Blocks

### `send#atomic_swap_delegation` block

#### `permit_swap_representative`
|             | header          | asset height | receive height | min raw (inclusive)             |
| ----------- | --------------- | ------------ | -------------- | ------------------------------- |
| hex length  | 13 chars        | 10 chars     | 10 chars       | 31 chars                        |
| hex         | 59989C359E22C   | 0000000003   | 000000002F     | 0000017FB3B29F21F77C409E0000000 |
| value       | ban_1permitswap | block 3      | block 47       | 19 BAN                          |

Note that the hex the same structure as the `atomic_swap_representative` but with a different header.


### `receive#atomic_swap_delegation` block

Any Banano block receiving `send#atomic_swap_delegation` at block height `receive height` is a `receive#atomic_swap_delegation` block.


## Validation

`asset height` in `send#atomic_swap_delegation` must refer to a valid head block for an asset.

`block height` for `receive#atomic_swap_delegation` must match `receive height` in `send#atomic_swap_delegation`.

`receive#atomic_swap_delegation` must be immediately followed by a valid `send#atomic_swap` block or the delegation is considered cancelled.

The `send#atomic_swap` must have equal or greater value of `min raw` compared to `min raw` in `send#atomic_swap_delegation`.

The atomic swap procedure must be valid according to the `atomic_swap` specification.

Any `send#atomic_swap` chain that is conclusively cancelled must be immediately followed by a new valid `send#atomic_swap` or the delegation is considered cancelled.
