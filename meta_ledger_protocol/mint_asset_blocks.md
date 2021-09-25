# Mint Asset Blocks

Several different types of blocks can mint an asset with different behaviour.


## `change#mint_asset`

A change block with the `representative` field set to an `nft_template_representative`.

This block will mint an asset in the issuer account.


## `send#mint_asset`

A send block with the `representative` field set to an `nft_template_representative`.

This block will mint an asset and send it.
