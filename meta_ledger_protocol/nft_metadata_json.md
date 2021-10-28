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
    "nft_supply_block_hash": "F61A79F286ABC5CC01D3D09686F0567812B889A5C63ADE0E82DD30F3B2D96463",
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

The `nft_supply_block_hash` must refer to an `#nft_supply` block followed by a `#mint_asset` block for this metadata.

The value of `"issuer"` must match the `account` field on the `#nft_supply` block and `#mint_asset` blocks.
