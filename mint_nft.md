# Meta network NFTs on Banano

## Subscribe account to meta nodes
Sending to the subscribe address will add the sending account to a watch list on the meta nodes.

Any change blocks will be inspected to see if they contain a command on IPFS.
```
send#subscribe
recipient: ban_1metanodesubscription1111111111111111111111111111111hx48xsub
```

## Mint NFT
```
change#ipfs
recipient: IPFS CID for NFT on-chain properties
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
  "title": "Camo Banano Volcano",
  "issuer": "ban_1coranoshiqdentfbwkfo7fxzgg1jhz6m33pt9aa8497xxfageuskroocdxa",
  "max_supply": "1",
  "ifps_cid": "QmbzTMo42KADUbLwc43KR9Se6aV3N6wfKqFbSr2qN1gJqR",
  "mint_previous": "F61A79F286ABC5CC01D3D09686F0567812B889A5C63ADE0E82DD30F3B2D96463"
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
    "title": {
      "type": "string",
      "title": "NFT schema title",
      "description": "A short human-friendly text to help identify the NFT schema.",
      "minLength": 1,
      "maxLength": 255
    },
    "mint_previous": {
      "type": "string",
      "title": "Previous block hash for the mint block.",
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
  required: ["command", "version", "title", "mint_previous", "issuer"]
}
```

### NFT data

Data that can be fetched by the client that isn't required by the meta node.
The IPFS CID is stored in `ipfs_cid` in NFT on-chain properties.

### JSON Example

```
{
  "description": "Image of Coranos painting a volcano that becomes a real volcano.",
  "image_ipfs_cid": "QmbzTMo42KADUbLwc43KR9Se6aV3N6wfKqFbSr2qN1gJqR",
  "tips": [
    {
      "title": "Coranos",
      "account": "ban_1coranoshiqdentfbwkfo7fxzgg1jhz6m33pt9aa8497xxfageuskroocdxa"
    }
  ]
}
```
