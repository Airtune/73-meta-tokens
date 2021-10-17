# `#nft_supply` block

An `#nft_supply` block is any block with a `nft_supply_representative` set in the `representative` field.

`change#nft_supply`

`send#nft_supply`

`receive#nft_supply`


## nft_supply_representative

`header` is used for detecting `#nft_supply` blocks.

`MAJOR version`, `MINOR version`, and `PATCH version` is used for semantic versioning of the meta ledger protocol.

`max supply` is used for max supply of NFTs. Use 0 for unlimited supply.

|             | header                  | MAJOR version  | MINOR version | PATCH version | max supply       |
| ----------- | ----------------------- | -------------- | ------------- | ------------- | ---------------- |
| hex length  | 18 chars                | 10 chars       | 10 chars      | 10 chars      | 16 chars         |
| hex         | 51BACEED6078000000      | 0000000000     | 0000000001    | 0000000000    | 000000000000076C |
| value       | ban_1nftsupp1y11111     | 0              | 1             | 0             | 1900             |


### Example:

Public key:
`51BACEED60792CA432000000000100000000010000000000000000000000076C`

Account:
`ban_1nftsupp1y1111111111111i1111111i111111111111111113uekda3b1jh`


## Usage

The block immediately following the `#nft_supply` block, at `#nft_supply block height + 1`, is interpreted as a `#mint_asset` block.

The `representative` field is interpreted as a `nft_template_representative` regardless of it's value.


### `#nft_supply_cancel` after `#nft_supply` block is confirmed

Submit a block with `ban_1nftsupp1ycance1111oops1111that1111was1111my1111bad1hq5sjhey` in the `representative` field immediately following the `#nft_supply` block.


## Validation

* `nft_supply_representative` must match header: `ban_1nftsupp1y11111`

* Version must be supported by the meta node.

* Must be followed by a block that isn't a `#nft_supply_cancel` block.

* Must be followed by a block that changes representative.
