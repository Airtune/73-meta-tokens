# Atomic Swap Meta Ledger Protocol

Atomic swap between Banano and an asset.

## Blocks

### `send#atomic_swap`

A send block that has data encoded in the representative public key hex value.

The amount of raw or Banano sent is irrelevant so 1 raw is recommended.


#### `atomic_swap_representative`

Representative field can be represented as a 64-char hex. The hex is split into segments encoding requirements for the atomic swap.

`ban_1atomicswap` is used as a header to detect `send#atomic_swap` blocks containing encoded requirements.

`asset height` is the Banano block height for the frontier block of the asset to swap. The `asset height` can also refer to a `receive#atomic_swap_delegation` block. For more details see `atomic_swap_delegation`.

`receive height` is the recipient's current account block height + 1.

`min raw` is the minimum amount of raw to send back for the swap to be valid.

|             | header          | asset height | receive height | min raw (inclusive)             |
| ----------- | --------------- | ------------ | -------------- | ------------------------------- |
| hex length  | 13 chars        | 10 chars     | 10 chars       | 31 chars                        |
| hex         | 23559C159E22C   | 0000000001   | 00000001CA     | 0000017FB3B29F21F77C409E0000000 |
| value       | ban_1atomicswap | block 1      | block 458      | 19 BAN                          |

Example: `ban_1atomicswap11111111i111119711113hysu79s3yxy639i11111cquj6wdh`

----

### `receive#atomic_swap`

Any Banano block receiving `send#atomic_swap` at block height `receive height` is a `receive#atomic_swap` block.


#### `change#abort_receive_atomic_swap`

To cancel the swap while `receive#atomic_swap` isn't confirmed in the Banano ledger.

`change#abort_receive_atomic_swap` has the block height `receive height` with the same `previous` value as `previous` from `receive#atomic_swap`.

----

### `send#payment`

Any Banano block at blockheight `receive height + 1` immediately following `receive#atomic_swap` that is sending a payment to the original owner of the asset prior to the swap.

For an `atomic_swap_delegation` the original owner is the delegator, not the delegatee.


#### `change#abort_payment`

To cancel the swap while `receive#atomic_swap` is confirmed but `send#payment` isn't.

`change#abort_payment` has the block height `receive height + 1` with `previous` set to the block hash of `receive#atomic_swap`.

----

### `receive#payment`

Normal Banano receive.

Changing representative back to a real representative in this block is recommended.


### Behaviour

#### Validation of Atomic Swaps

`send#atomic_swap` representative hex value must be a valid Atomic Swap Representative HEX.

`send#atomic_swap` amount must be 1 raw.

`send#atomic_swap` must be confirmed.

`send#atomic_swap` must not be a send to self, e.g. link must not match sender account.

`asset height` in `send#atomic_swap` must refer to the valid frontier Banano block for an asset meta chain or a valid `receive#atomic_swap_delegation` block.

`receive#atomic_swap` must be confirmed with block height `receive height`.

`receive#atomic_swap` must not change representative.

`receive height` must be greater than 1, i.e., the receive block must not be an open block.

Account balance at `receive height - 1` must be greater than `min raw`.

`send#payment` must be confirmed with block height `receive height + 1`.

`send#payment` must be sent to the account that submitted `send#atomic_swap`.

`send#payment` amount of raw must be equal to or larger than `min raw`.

`send#payment` must not change representative.

`send#payment` must be valid and come before any other action for the other action to be allowed. Following actions can be: `send#asset`, `send#atomic_swap`, or `send#atomic_swap_delegation`.

#### Locked Asset

The asset is locked after `send#atomic_swap` is confirmed while the atomic swap isn't validated or invalidated yet.

While the asset is locked it is still owned by the sender account but attempts at sending it will be undetermined until the atomic swap has been concluded.


##### Locked Asset Example 1

There's no confirmed block in recipient account at `receive height`.


##### Locked Asset Example 2

`receive#atomic_swap` is confirmed but there's no confirmed block at `receive height + 1` in the recipient account.


##### Attempting to send a locked asset

Trying to send a locked asset will make chains on light nodes for the asset that are undetermined until the atomic swap has been concluded.

If the atomic swap was successful then `send#atomic_swap` is treated as a valid send. Subsequent sends will be ignored.

If the atomic swap was unsuccessful then `send#atomic_swap` is ignored. The first subsequent send is now valid.


### Limitations

#### Account height limit
```
10 char hex
0xFFFFFFFFFF
1,099,511,627,775
~1 trillion blocks limitation for a single account
```

For comparison the height for F@H account was 2,878,435 blocks at 2021-08-14.


#### Highest amount for min raw
```
31 char hex
0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
21267647932558653966460912964485513215 raw
~212.67 million BAN ceiling for atomic swaps
```

Only giveaway funds have amounts of BAN that large.
