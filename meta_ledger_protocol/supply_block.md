# `#supply` block

A `#supply` block is any block with a `supply_representative` set in the `representative` field.

`change#supply`

`send#supply`

`receive#supply`


## supply_representative

`header` is used for detecting `#supply` blocks.

`MAJOR version`, `MINOR version`, and `PATCH version` is used for semantic versioning of the meta ledger protocol.

`max supply` is used for max supply of NFTs. Use 0 for unlimited supply.

|             | header                  | MAJOR version  | MINOR version | PATCH version | max supply       |
| ----------- | ----------------------- | -------------- | ------------- | ------------- | ---------------- |
| hex length  | 18 chars                | 10 chars       | 10 chars      | 10 chars      | 16 chars         |
| hex         | 51BACEED6078000000      | 0000000000     | 0000000001    | 0000000000    | 000000000000076C |
| value       | ban_1nftsupp1y11111     | 0              | 1             | 0             | 1900             |


### Example:

Public key:
`51BACEED6078000000000000000000000000010000000000000000000000076C`

Account:
`ban_1nftsupp1y111111111111111111111i111111111111111113ue4ziwpt86`


## Usage

The block immediately following the `#supply` block, at `#supply block height + 1`, is interpreted as a `#mint` block.

The representative of the first mint block is used as the `asset_representative`.


### `#cancel_supply` after `#supply` block is confirmed

Submit a block with `ban_1nftsupp1ycance1111oops1111that1111was1111my1111bad1hq5sjhey` in the `representative` field immediately following the `#supply` block.

Submitting a block with the header: `ban_1nftsupp1y11111...` will also function as a cancel block for the previous `#supply` block


## Validation

* `supply_representative` must match header: `ban_1nftsupp1y11111`

* Meta protocol version must be supported by the meta node.

* Must be followed by a block that isn't a `#cancel_supply` block or a `#supply` block.

* Must be followed by a block that changes to representative that isn't a `supply_representative`.

* If `max supply` is 0 then the supply is unlimited.
