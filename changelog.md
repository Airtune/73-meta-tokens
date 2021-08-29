# Changelog

## v0.1.0

Split specification into multiple files.
Separated `meta_node_api`, `meta_ledger_protocol`, and `client_protocol`.

`meta_node_api` is the API for getting ownership info from meta nodes.

`meta_ledger_protocol` is the protocol for how assets are stored, minted, and transferred in the Banano ledger.

`meta_client_protocol` is protocols for things such as how clients verify assets and conduct atomic swaps.


## Atomic swaps without Musig

Added specifications for an atomic swap algorithm the doesn't require Musig.

Read more in:

`meta_ledger_protocol/atomic_swap.md`

`meta_client_protocol/atomic_swap.md`


## Remove NFT Template blocks.

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
