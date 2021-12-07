# `#supply` block

A `change#supply` block has a `supply_representative` set in the `representative` field.


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

The block immediately following the `change#supply` block, at `change#supply block height + 1`, is interpreted as a `#mint` block.

The representative of the first mint block is used as the `metadata_representative`.


### `#cancel_supply` after `change#supply` block is confirmed

Submit a block with `ban_1nftsupp1ycance1111oops1111that1111was1111my1111bad1hq5sjhey` in the `representative` field immediately following the `change#supply` block.

Submitting a block with the header for a supply_representative, finish_supply_representative, or atomic_swap_representative will also function as a cancel block for the previous `change#supply` block.


### `#finish_supply` block

Makes it so that no new NFTs can be minted from a `change#supply` block by putting a `finish_supply_representative` in the `representative` field of any block with block height higher that the supply block.

#### `finish_supply_representative`

|             | header                   | supply block height                      |
| ----------- | ------------------------ | ---------------------------------------- |
| hex length  | 24 chars                 | 40 chars                                 |
| hex         | 3614865E0051BA0033BB581E | 0000000000000000000000000000000000000002 |
| value       | ban_1finish11nft11supp1y | 2                                        |

Example: `ban_1finish11nft11supp1y11111111111111111111111111111114ig649dj3`


## Validation

* `supply_representative` must match header exactly: `ban_1nftsupp1y11111`

* Meta protocol version must be supported by the meta node.

* Banano block subtype must be `change`.

* Must be followed by a block doesn't have the `cancel_supply_representative`.

* Must be followed by a block doesn't have the `supply_representative` header.

* Must be followed by a block doesn't have the `finish_supply_representative` header.

* Must be followed by a block doesn't have the `atomic_swap_representative` header.

* If `max supply` is 0 then the supply is unlimited.
