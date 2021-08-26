# NFT Template

The NFT template is stored on meta nodes for operational purposes while metadata might not be stored be stored on meta nodes.


## `change#nft_template` block

A change block `change#nft_template` with an `nft_template_json_representative`.

The `nft_template_json_representative` should not be confused with the `nft_template_block_representative` used in Asset First Send.


### `nft_template_json_representative`

IPFS v0 CID for an `nft_template.json` encoded as a Banano account.


#### IPFS v0 CID to Banano account

1) The v0 CID is converted from base58 to hex.

2) The `1220` prefix is stripped from the hex.

3) The stripped hex is used as a Banano public to to convert it into a Banano account.


#### Banano account to IPFS v0 CID

1) Extract the hex public key from the Banano account.

2) Prepend `1220` to the public key to convert it to a hex CID.

3) Convert the hex CID to base58.


## `nft_template.json` example

```
{
  "command": "nft_template",
  "version": "0.1.0",
  "title": "Camo Banano Volcano",
  "issuer": "ban_1coranoshiqdentfbwkfo7fxzgg1jhz6m33pt9aa8497xxfageuskroocdxa",
  "max_supply": "1",
  "metadata_ipfs_cid": "QmbzTMo42KADUbLwc43KR9Se6aV3N6wfKqFbSr2qN1gJqR",
  "previous": "F61A79F286ABC5CC01D3D09686F0567812B889A5C63ADE0E82DD30F3B2D96463"
}
```


## Validation

The `change#nft_template` block must be confirmed.

The `previous` field in the `change#nft_template` block must match `previous` in `nft_template.json`.

The `account` field in the `change#nft_template` block must match `issuer` in `nft_template.json`.

The `version` in `nft_template.json` must be supported by the meta node.

The `command` must be `"nft_template"`.

If the key `max_supply` isn't present then the supply is unlimited.

If the key `max_supply` is present then the value must be a valid integer equal to or higher than `1`.


### `nft_template.json` JSON Schema
```
{
  "title": "Make an NFT template",
  "description": "Minimal JSON representation of NFT on-chain properties.",
  "type": "object",
  "properties": {
    "command": {
      "type": "string",
      "title": "Command to be executed by meta node.",
      "description": "Possible commands: nft_template",
      "pattern": "nft_template"
    },
    "version": {
      "type": "string",
      "title": "Version of protocol",
      "description": "Used to distinguish between different versions of the meta command protocol.",
      "minLength": 5,
      "maxLength": 255
    },
    "title": {
      "type": "string",
      "title": "NFT template title",
      "description": "A short human-friendly text to help identify the NFT template.",
      "minLength": 1,
      "maxLength": 255
    },
    "previous": {
      "type": "string",
      "title": "Previous block hash for the template block.",
      "minLength": 64,
      "maxLength": 64
    },
    "issuer": {
      "type": "string",
      "title": "Account minting the NFT on Banano. Used for verification during minting.",
      "minLength": 64,
      "maxLength": 64
    },
    "max_supply": {
      "type": "string",
      "description": "Max supply limit. If this property isn't present the supply is unlimited.",
      "minLength": 1,
      "maxLength": 39
    },
    "metadata_ipfs_cid": {
      "title": "IPFS CID for NFT metadata",
      "description": "ERC-721 or ERC-1155 compliant Metadata JSON",
      "type": "string"
    }
  },
  required: ["command", "version", "title", "previous", "issuer"]
}
```
