# Mint Blocks

Several different types of blocks can a mint block with different behaviour.

A mint block must immediately follow the `#supply` block.


## `change#mint`

A change block with the `representative` field set to an `asset_representative`.

This block will mint an asset in the issuer account.

This block's hash will be used for the `asset_representative`.


## `send#mint`

A send block with the `representative` field set to an `asset_representative`.

This block will mint an asset and send it.

This block's hash will be used for the `asset_representative`.
