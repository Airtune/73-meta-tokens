# Atomic Swap

## `send#atomic_swap`

A send block `send#atomic_swap` that has the representative hex value set to Atomic Swap Representative HEX.

The amount of raw or Banano sent is irrelevant so 1 raw is recommended.


### Atomic Swap Representative HEX

Representative field can be represented as a 64-char hex. The hex is split segments encoding requirements for a swap.

`ban_1atomicswap` is used as a header to detect `send#atomic_swap` blocks followed by encoded data.

`asset height` is the block height for the frontier receive block for the asset.

`receive height` is the recipient account block height + 1.

`min raw` is the minimum amount of raw to send back for the swap to be valid. The payment block must immediatly follow the `receive#atomic_swap` since any other send/receive/change block will cancel the swap.

|             | header        | asset height | receive height | min raw                         |
| ----------- | ------------- | ------------ | -------------- | ------------------------------- |
| hex length  | 13 chars      | 10 chars     | 10 chars       | 31 chars                        |
| hex         | 23559C159E22C | 0000000003   | 000000002F     | 0000017FB3B29F21F77C409E0000000 |
| value       | 1atomicswap   | block 3      | block 47       | 19 BAN                          |


## `receive#atomic_swap`

Any Banano block receiving `send#atomic_swap` at blockheight `receive height` is a `receive#atomic_swap` block.


## `send#payment`

Any Banano block at blockheight `receive height + 1` immediatly following `receive#atomic_swap` that is paying the sending account of `send#atomic_swap` .


## `receive#payment`

Normal Banano receive.

Changing representative back to a real representative in this block is recommended.


### Behaviour

#### Validation of Atomic Swaps

`send#atomic_swap` representative hex value must be a valid Atomic Swap Representative HEX.

`send#atomic_swap` must be confirmed.

`asset height` in `send#atomic_swap` must refer to a receive block for an asset that is the valid frontier prior to `send#atomic_swap` in the same account.

`receive#atomic_swap` must be confirmed with blockheight `receive height`.

`send#payment` must be confirmed with blockheight `receive height + 1`.

`send#payment` must have `link` set to the sender of `send#atomic_swap`.

`send#payment` amount of raw must be equal to or larger than `min raw`.


#### Locked Asset

The asset is locked after `send#atomic_swap` is confirmed while the atomic swap isn't validated or invalidated yet.

While the asset is locked it is still owned by the sender account but attempts at sending it will be undetermined until the atomic swap has been concluded.


##### Locked Asset Example 1

There's no confirmed block in recipient account at `receive height`.


##### Locked Asset Example 2

`receive#atomic_swap` is confirmed but there's no confirmed block at `receive height + 1` in the recipient account.


##### Attempting to send a locked asset

Trying to send a locked asset will make chains for the asset in the sender account that are undetermined until the atomic swap has been concluded.

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
