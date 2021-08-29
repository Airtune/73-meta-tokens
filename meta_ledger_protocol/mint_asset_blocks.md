# Mint Asset Blocks

Several different types of blocks can mint an asset with different behaviour.


## `change#mint_asset`

A change block with the `representative` field set to an `nft_template_representative`.

This block will mint an asset in the issuer account.


## `send#mint_asset`

A send block with the `representative` field set to an `nft_template_representative`.

This block will mint an asset and send it.


## (`receive#mint_asset` ***EXPERIMENTAL***)

A receive block with the `representative` field set to an `nft_template_representative`.

This block will mint an asset in the recepient account with ownership set to the linked send block account when `receive#mint_asset` is confirmed.

This will transfer ownership from the receiver to the sender.
