# Mint Asset Blocks

Several different types of blocks can mint an asset with different behaviour.

A mint asset block must immediately follow the `#nft_supply` block.


## `change#mint_asset`

A change block with the `representative` field set to an `nft_metadata_representative`.

This block will mint an asset in the issuer account.

This block's hash will be used for the `asset_representative`.


## `send#mint_asset`

A send block with the `representative` field set to an `nft_metadata_representative`.

This block will mint an asset and send it.

This block's hash will be used for the `asset_representative`.
