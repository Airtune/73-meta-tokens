## Client Atomic Swap Algorithm:
### 0) Setup
* A and B shares all blocks, unsigned, with each other and agree to the trade.


### 1) Sign and share cancel blocks
  * B signs `change#abortB` and shares the signed block with A
  * A signs `send#primeif`, `change#abortA`, `change#cancelA` and shares the signed blocks with B

A and B can now submit `change#abortA` to abort the trade and invalidate `send#primeif`.

A and B can now submit `change#abortB` to abort the trade and invalidate `send#19BAN`.

A and B can now submit `send#primeif` to prime the trade.


### 2) A or B submits `send#primeif` and wait for confirmation.

A and B can now submit `change#cancelA` to cancel the trade and invalidate `send#assetif`


### 3) B submits `send#assetif` and A waits for `send#assetif` confirmation.

If A is unresponsive, B submits `change#abortB` to cancel the trade.

If A submits any other send/receive/change block than `send#19BAN`, the trade is cancelled.


### 4) When `send#assetif` is confirmed, A submits `send#19BAN hash: 25`

When `send#19BAN hash: 25` is confirmed then `send#assetif` becomes a valid asset send.


### 5) A submits `receive#asset` like normal to receive the asset
