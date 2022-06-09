# Changelog

## v1.0.0 release

Removed delegated atomic swaps. The protocol is now accepted as is and has been tested in production.

## v0.1.0 proposal 4

Added a `#finish_supply`. Finish off a `#supply` block so no more NFTs can be minted.


## v0.1.0 proposal 3

```
rename mint_asset                  -> mint
rename nft_metadata_json           -> metadata_json
rename nft_metadata_representative -> metadata_representative
rename nft_metadata_ipfs_cid       -> metadata_ipfs_cid
rename nft_supply                  -> supply
rename nft_supply_block            -> supply_block
rename nft_supply_block_hash       -> supply_block_hash
rename nft_supply_representative   -> supply_representative
rename nft_supply_cancel           -> cancel_supply
```

A `#supply` block can be cancelled both by being followed by a `#cancel_supply` block or by another `#supply` block.


## v0.1.0 proposal 2

### Introduce `nft_supply_block`

To make the protocol support Nano light nodes, using an `nft_supply_block` in-ledger will allow making an implementation that only need to process blocks once.


### Merge `nft_template_json` and `nft_metadata_json` into `nft_metadata_json`

Now that all data relevant for the meta node to calculate owner ship is in-ledger instead of in `nft_template_json`, separation of `nft_template_json` and `nft_metadata_json` is no longer necessary.


### Use IPFS CID for `nft_metadata_json` as the `asset_representative`

The `nft_supply_block` must be followed by the first mint block containing the `asset_representative` in the `representative` field of the block.


## v0.1.0 proposal 1

Split specification into multiple files.
Separated `meta_node_api`, `meta_ledger_protocol`, and `client_protocol`.

`meta_node_api` is the API for getting ownership info from meta nodes.

`meta_ledger_protocol` is the protocol for how assets are stored, minted, and transferred in the Banano ledger.

`meta_client_protocol` is protocols for things such as how clients verify assets and conduct atomic swaps.


### Atomic swaps without Musig

Added specifications for an atomic swap algorithm the doesn't require Musig.

Read more in:

`meta_ledger_protocol/atomic_swap.md`

`meta_client_protocol/atomic_swap.md`


### Remove NFT Template blocks.

`nfttemplate` blocks have been removed in favor of minting 1 asset following `previous` in `nft_template.json` instead.


### Naming changes

#### ~~NFT on-chain properties~~ -> nft_template, nft_template.json, nft_template_ipfs_cid

Changed for consistent naming.

----

#### ~~art_data~~ -> metadata
#### ~~art_data.json~~ -> metadata.json
#### ~~art_data_ipfs_cid~~ -> metadata_ipfs_cid

Changed for consistent naming and compatability with ERC-721 or ERC-1155 Metadata JSON.

----

#### ~~send#assetif~~ -> send#atomic_swap
#### ~~receive#assetif~~ -> receive#atomic_swap

Changed for consistent naming.
