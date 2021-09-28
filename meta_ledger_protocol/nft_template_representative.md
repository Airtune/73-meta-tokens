# `nft_template_representative`

Banano account with an IPFS v0 CID with `nft_template_json` encoded in it. Used in `#mint_asset` blocks.


## IPFS v0 CID to Banano account

1) The v0 CID is converted from base58 to hex.

2) The `1220` prefix is stripped from the hex.

3) The stripped hex is used as a Banano public key to convert it into a Banano account.


## Banano account to IPFS v0 CID

1) Extract the hex public key from the Banano account.

2) Prepend `1220` to the public key to convert it to a hex CID.

3) Convert the hex CID to base58.
