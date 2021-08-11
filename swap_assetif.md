# Accounts
`Account A has 1 asset   frontier hash: 3`

`Account B has 19 BAN    frontier hash: 24`


# Blocks

Account B blocks:
* `change#abortB   previous: 24  hash: 0`
* `send#19BAN      previous: 24  hash: 25  recipient: A`
* `receive#asset   previous: 25`


Account A blocks:
* `send#prime      previous: 3   hash: 4   recipient: asset   representative: hash 25`
* `send#assetif    previous: 4   hash: 5   recipient: B       representative: asset`

* `change#abortA   previous: 3   hash: 6`
* `change#cancelA  previous: 4   hash: 7`


# Block explanations

## Account A `send#prime`
This block comes before `send#assetif`. It changes the properties of `send#assetif` from a normal
send to a conditional send.

`send#assetif` will only be valid after `send#19BAN previous: 24 hash: 25` has been confirmed.


## Account B `change#abortB`
Can be any block that is not `send#19BAN` with `previous: 24`.
Any confirmed block other than `send#19BAN` for `previous: 24` will abort the trade.


## Account B `change#abortA` and `change#cancelA`

Cancels the trade when confirmed by making sure `send#assetif` could never be confirmed.


# Algorithm:
## 0) Setup
* A and B shares all blocks, unsigned, with each other and agree to the trade.


## 1) Sign and share cancel blocks
  * B signs `change#abortB` and shares the signed block with A
  * A signs `send#prime`, `change#abortA`, `change#cancelA` and shares the signed blocks with B

A and B can now submit `change#abortA` to abort the trade and invalidate `send#prime`.

A and B can now submit `change#abortB` to abort the trade and invalidate `send#19BAN`.

A and B can now submit `send#prime` to prime the trade.


## 2) A or B submits `send#prime` and wait for confirmation.

A and B can now submit `change#cancelA` to cancel the trade and invalidate `send#assetif`


## 3) B submits `send#assetif` and A waits for `send#assetif` confirmation.

If A is unresponsive, B submits `change#abortB` to cancel the trade.

If A submits any other send/receive/change block than `send#19BAN`, the trade is cancelled.


## 4) When `send#assetif` is confirmed, A submits `send#19BAN hash: 25`

When `send#19BAN hash: 25` is confirmed then `send#assetif` becomes a valid asset send.


## 5) A submits `receive#asset` like normal to receive the asset
