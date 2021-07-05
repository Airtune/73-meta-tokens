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

Minimal properties of on-chain behaviour and a link to NFT data on IPFS like tip addresses, description, and art.

### JSON Example

```
{
  "command": "mint_nft",
  "version": "0.0.0",
  "title": "Banano with Apple market cap",
  "issuer": "ban_3airtunegymgr6b8t9b8muh7upg39bcheahxqwkbtu96ux69pzn1idcu34wz",
  "max_supply": "1900",
  "ifps_cid": "QmSexmL78HCBZh4BCH2A3vgo3WFvrhoQgQTKGMwtsgvhjw"
}
```

#### JSON Schema
```
{
  "title": "Mint NFT meta command",
  "description": "Minimal JSON representation of the on-chain properties.",
  "type": "object",
  "properties": {
    "command": {
      "type": "string",
      "title": "Command to be executed by meta node.",
      "description": "Possible commands: mint_nft",
      "pattern": "mint_nft"
    },
    "version": {
      "type": "string",
      "title": "Version of protocol",
      "description": "Used to distinguish between different versions of the meta command protocol.",
      "minLength": 5,
      "maxLength": 255
    },
    "schema_title": {
      "type": "string",
      "title": "NFT schema title",
      "description": "A short human-friendly text to help identify the NFT schema.",
      "minLength": 1,
      "maxLength": 255
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
    }
  },
  required: ["title", "issuer"]
}
```

### NFT data

Data that can be fetched by the client that isn't required by the meta node.

### JSON Example

```
{
  "description": "Image of the unlikely event that Banano will exceed Apple's market capitalization.",
  "image_ipfs_cid": "QmSexmL78HCBZh4BCH2A3vgo3WFvrhoQgQTKGMwtsgvhjw",
  "tips": [
    {
      "title": "Original taker of screenshot: Airtune.",
      "account": "ban_3airtunegymgr6b8t9b8muh7upg39bcheahxqwkbtu96ux69pzn1idcu34wz"
    }
  ]
}
```
