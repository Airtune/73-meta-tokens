# Atomic Swap Delegation Client Protocol

## Introduction

Atomic Swap Delegation provides an alternative to custodial exchange between NFTs and BAN.

Instead of a `custodial account` there's a `delegatee account` that is granted permission by the NFT `seller account` to place a lock on an NFT asset during an atomic swap.

With Atomic Swap Delegation, the ownership of the NFT remains with the `seller account` until the swap is done, the payment goes directly from the `buyer account` to the `seller account`, and the NFT ownership goes directly from the `seller account` to the `buyer account`.

At no point does the `delegatee account` hold BAN or NFT assets.

Since the `delegatee account` holds neither NFT assets or BAN, there's little incentive to hack the delegatee. The delegatee is also unable exit scam and is put in a position where it's unfavorable to enforce fees.


## Vulnerabilities

### Adversary delegatee locks NFT Asset

It's not entirely trustless since it relies on the NFT asset being locked by the `delegatee account` during a swap.

An adversary `delegatee account` is able to simply create a new account, initiate an atomic swap, and never release the lock. The NFT will be locked and ownership will remain in the `seller account` indefinitely.


### Delegatee goes offline indefinitely during a swap

If the delegatee goes offline, then sellers should be able to recover their NFTs.

In the case that their NFT asset is locked by the `delegatee account` and the `buyer account` is unresponsive, the NFT asset could potentially be locked in the `seller account` indefinitely.
