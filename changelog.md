# Changelog

## v0.1.0

Split specification into multiple files.
Separated `meta_node_api`, `meta_node_protocol`, and `client_protocol`.

`meta_node_api` is the API for getting ownership info from meta nodes.

`meta_ledger_protocol` is the protocol for how template and asset data is stored in the Banano ledger and validated.

`meta_client_protocol` is protocols for things such as how clients verify assets and conduct atomic swaps.

## Atomic swaps without Musig

Added specifications for an atomic swap algorithm the doesn't require Musig.

Read more in:

`meta_ledger_protocol/atomic_swap.md`

`meta_client_protocol/atomic_swap.md`

### Naming changes

#### ~~Mint NFT~~

Use `asset_first_send` and `nft_template` instead to avoid confusion.

----

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

----

#### ~~send#nfttemplate~~ -> change#nft_template
#### ~~receive#nfttemplate~~ -> change#nft_template

New requirement that `nft_template` blocks must be `change` blocks to future proof the protocol for Banano light nodes and meta nodes that only ever process each block once.
