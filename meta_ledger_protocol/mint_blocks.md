# Mint Blocks

Several different types of blocks can a mint block with different behaviour.

A mint block must immediately follow the `#supply` block.


## `change#mint`

A change block with the `representative` field set to an `metadata_representative`.

This block will mint an asset in the issuer account.

This block's hash will be used for the `asset_representative`.


## `send#mint`

A send block with the `representative` field set to an `metadata_representative`.

This block will mint an asset and send it.

This block's hash will be used for the `asset_representative`.

## `metadata_representative` validation

* Must not be a `cancel_supply_representative`.

* Must not match the `supply_representative` header.

* Must not match the `finish_supply_representative` header.

* Must not match the `atomic_swap_representative` header.

* Must not match the `atomic_swap_delegation_representative` header.

* Must not be one of these burn account:
  ```
  ban_1burnbabyburndiscoinferno111111111111111111111111111aj49sw3w
  ban_1uo1cano1bot1a1pha1616161616161616161616161616161616p3s5tifp
  ban_1ban116su1fur16uo1cano16su1fur16161616161616161616166a1sf7xw
  ban_1111111111111111111111111111111111111111111111111111hifc8npp
  ```