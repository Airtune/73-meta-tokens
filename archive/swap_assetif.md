## Accounts
`Account A has 1 asset   frontier hash: 3`

`Account B has 19 BAN    frontier hash: 24`


## Blocks

Account B blocks:
* `change#abortB   previous: 24  hash: 0`
* `send#19BAN      previous: 24  hash: 25  recipient: A`
* `receive#asset   previous: 25`


Account A blocks:
* `send#primeif    previous: 3   hash: 4   recipient: asset   representative: hash 25`
* `send#assetif    previous: 4   hash: 5   recipient: B       representative: asset`

* `change#abortA   previous: 3   hash: 6`
* `change#cancelA  previous: 4   hash: 7`


## Block explanations

### Account A `send#primeif`
This block comes before `send#assetif`. It changes the properties of `send#assetif` from a normal
send to a conditional send.

`send#assetif` will only be valid after `send#19BAN previous: 24 hash: 25` has been confirmed.


### Account B `change#abortB`
Can be any block that is not `send#19BAN` with `previous: 24`.
Any confirmed block other than `send#19BAN` for `previous: 24` will abort the trade.


### Account B `change#abortA` and `change#cancelA`

Cancels the trade when confirmed by making sure `send#assetif` could never be confirmed.
