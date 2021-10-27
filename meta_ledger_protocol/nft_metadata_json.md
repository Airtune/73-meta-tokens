## Metadata (ERC-721 or ERC-1155 Metadata JSON)

Data for the client that isn't required by the meta node.

The IPFS CID for the JSON is encoded in the nft_metadata_representative.


### JSON Example

```
{
  "name: "Inception",
  "description": "Image of Coranos painting a volcano that becomes a real volcano.",
  "image": "ipfs://QmbzTMo42KADUbLwc43KR9Se6aV3N6wfKqFbSr2qN1gJqR",
  "properties": {
    "issuer": "ban_1coranoshiqdentfbwkfo7fxzgg1jhz6m33pt9aa8497xxfageuskroocdxa",
    "tips": [
      {
        "name": "Coranos",
        "account": "ban_1coranoshiqdentfbwkfo7fxzgg1jhz6m33pt9aa8497xxfageuskroocdxa"
      }
    ]
  }
}
```

## Validation

The `previous` block must be a `#nft_supply` block followed by a `#mint_asset` block for this metadata.

The `previous` block must match the validation specified in `nft_supply_block`.

The value of `"issuer"` must match the `account` field on the `#mint_asset` blocks.
