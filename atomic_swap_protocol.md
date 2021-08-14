## `send#assetif`

### Representative HEX

Representative field can be represented as a 64-char hex. The hex is split segments encoding requirements for a swap.

`ban_1atomicswap` is used as a header to detect `send#assetif` blocks followed by encoded data.

`asset height` is the block height for the frontier receive block for the asset.

`receive height` is the recipient wallet block height + 1. `send#assetif` must be received at `receive height` for the swap to be valid.

`min raw` is the minimum amount of raw to send back for the swap to be valid. The payment block must immediatly follow the `send#assetif` since any other send/receive/change block will cancel the swap.

|             | header        | asset height | receive height | min raw                         |
| ----------- | ------------- | ------------ | -------------- | ------------------------------- |
| hex length  | 13 chars      | 10 chars     | 10 chars       | 31 chars                        |
| hex         | 23559C159E22C | 0000000003   | 000000002F     | 0000017FB3B29F21F77C409E0000000 |
| value       | 1atomicswap   | block 3      | block 47       | 19 BAN                          |

### Limitations

#### Wallet height limit
```
10 char hex
0xFFFFFFFFFF
1,099,511,627,775
~1 trillion blocks limitation for a single wallet
```

For comparison the height for F@H wallet was 2,878,435 blocks at 2021-08-14.


#### Highest amount for min raw
```
31 char hex
0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
21267647932558653966460912964485513215 raw
~212.67 million BAN ceiling for atomic swaps
```

Only giveaway funds have amounts of BAN that large.
