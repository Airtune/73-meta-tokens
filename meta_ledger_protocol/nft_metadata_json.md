## Metadata (ERC-721 or ERC-1155 Metadata JSON)

Data for the client that isn't required by the meta node.

The IPFS CID for this NFT Metadata is stored in `metadata_ipfs_cid` in `nft_template.json`.


### JSON Example

```
{
  "name: "Inception",
  "description": "Image of Coranos painting a volcano that becomes a real volcano.",
  "image": "ipfs://QmbzTMo42KADUbLwc43KR9Se6aV3N6wfKqFbSr2qN1gJqR",
  "properties": {
    "tips": [
      {
        "name": "Coranos",
        "account": "ban_1coranoshiqdentfbwkfo7fxzgg1jhz6m33pt9aa8497xxfageuskroocdxa"
      }
    ]
  }
}
```
