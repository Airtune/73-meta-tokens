# Meta network NFTs on Banano

## Mint NFT on Banano
```
change#priming
representative: ban_1mintnonfungib1etoken1919111111111111111111111111111wraarjmb

change#ipfs
representative: IPFS CID for NFT on-chain properties
```

## Send newly minted NFT
```
send#mint1
representative: change#ipfs block hash as address

send#mint2
representative: change#ipfs block hash as address
```

## Receive and send NFT
```
receive
link: send#mint2

send
representative: send#mint2 block hash as address used as NFT mint 2 ID
```

### NFT on-chain properties

### JSON Example

```
{
  "title": "Banano with Apple market cap",
  "issuer": "ban_3airtunegymgr6b8t9b8muh7upg39bcheahxqwkbtu96ux69pzn1idcu34wz",
  "max_supply": 1900,
  "backing_raw": 100000000000000000000000000,
  "ifps_cid": "QmSexmL78HCBZh4BCH2A3vgo3WFvrhoQgQTKGMwtsgvhjw",
  "recommended_tips": [
    {
      "account": "ban_3airtunegymgr6b8t9b8muh7upg39bcheahxqwkbtu96ux69pzn1idcu34wz",
      "amount_per_mille": 19
    }
  ]
}
```

#### JSON Schema
```
{
  "title": "NFT properties",
  "description": "JSON representation of the properties of a NFT.",
  "type": "object",
  "properties": {
    "title": {
      "type": "string",
      "title": "NFT title",
      "description": "A short human-friendly text to help identify the NFT type."
    },
    "issuer": {
      "type": "string",
      "title": "Account minting the NFT on Banano"
    },
    "max_supply": {
      "type": "integer",
      "description": "Max supply limit. If this property isn't present the supply is unlimited.",
      "minimum": 1,
      "maximum": 100_000_000_000.0
    },
    "backing_raw": {
      "title": "Backing",
      "description": "Specific amount of raw required to send NFT."
      "type": "integer",
      "minimum": 1,
      "default": 1
    },
    "ipfs_cid": {
      "title": "IPFS CID",
      "description": "For client to fetch NFT data like artwork, text, and meta data on IPFS.",
      "type": "string"
    },
    "hyperdrive_key": {
      "title": "Hyperdrive public key",
      "description": "For client to fetch NFT data like artwork, text, and meta data on Hypercore.",
      "type": "string"
    },
    "hyperdrive_discovery_key": {
      "title": "Hyperdrive discovery key",
      "description": "For client to find peers sharing the Hyperdrive on Hypercore.",
      "type": "string"
    },
    "recommended_tips": {
      "title": "List of addresses to recommend tipping during trades.",
      "type": "array",
      "items": {
        "type": "object",
        "items": {
          "properties": {
            "account": {
              "type": "string",
              "title": "Banano address to recommend tipping during trades."
            },
            "amount_per_mille": {
              "type": "integer",
              "title": "Recommended tip amount per mille for trades.",
              "minimum": 0,
              "maximum": 190
            }
          }
        }
      }
    }
  },
  required: ["title"]
}
```
