# Atomic Swap

A has an asset.

B has 19 BAN.

A and B want to swap the asset and 19 BAN.


## Client Atomic Swap Algorithm:

### 0) Setup

* A and B shares all blocks from `meta_ledger_protocol/atomic_swap.md`, unsigned, with each other and proceed if they both agree to the trade.


### 1) B signs and shares cancel blocks

  * B signs `change#abort_receive_atomic_swap`, `change#abort_payment` and shares the signed blocks with A

A and B can now submit `change#abort_receive_atomic_swap` to abort the trade and invalidate `send#atomic_swap`.

A and B can now submit `change#abort_payment` to abort the trade and invalidate `send#payment`.

A and B can now submit `send#primeif` to prime the trade.


### 2) A submits `send#atomic_swap`

A signs and submit the `send#atomic_swap`.

A and B can now submit `change#abort_receive_atomic_swap` to abort the trade and invalidate `send#atomic_swap`.

If B is unresponsive A submits `change#abort_receive_atomic_swap` to unlock the asset.


### 3) B submits `receive#atomic_swap`

After `receive#atomic_swap` has been confirmed, A and B can no longer submit `change#abort_receive_atomic_swap`.

A and B can now submit `change#abort_payment` to abort the trade and invalidate `send#atomic_swap`.

If B is unresponsive A submits `change#abort_payment` to unlock the asset.


### 4) B submits `send#payment`

After `receive#atomic_swap` has been confirmed, B submits `send#payment`.

Once `send#payment` is confirmed the Atomic Swap is complete, the asset is unlocked, and the asset ownership is transferred to B.


### 5) A submits `receive#payment`
