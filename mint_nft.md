# Meta NFTs on top of the Nano protocol

## Terminology

A "command" is short piece of data encoded on-chain to request performing an action on the meta ledger.

The "meta ledger" contains the NFT ownership histories calculated by a "meta node".

The term "meta data" refers to data for the NFT unrelated to on-chain behaviour, e.g., artwork and vanity names.

NFT "properties" are stored on-chain.

The "issuer" is the account submitting the mint NFT command.

## Mint NFT command

### Header1: commandBytesize <= 27
If the command can be encoded in 27 bytes or less it is stored in a single address.

Address header:
```
ban_1mintnft...
nano_1mintnft...
```

Hex header (5 bytes):
```
4E14D51BA0...
```

### Header3: commandBytesize >= 28 && commandBytesize <= 8218
If the command is 28 bytes or more it has to be encoded in at least 2 addresses.

Address header:
```
ban_3mintnft...
nano_3mintnft...
```

Hex header (6 bytes):
```
CE14D51BA0xx...
```
`xx` is replaced with the hex count of extra addresses needed to encode the command beyond the 2 default addresses.
The maximum amount of addresses is the 2 default + 255 extra for a total of 257 addresses.

### JSON Schema for properties
Note all properties are optional and minting NFTs without any properties, `{}`, would use default values.
```
{
  "title": "Mint NFT command",
  "description": "JSON representation of the parameters for minting a new type of NFT.",
  "type": "object",
  "properties": {
    "t": {
      "type": "string",
      "title": "Title",
      "description": "Human-friendly text stored on chain to help identify the NFT type while meta data isn't available."
    }
    "m": {
      "type": "integer",
      "description": "Max supply limit. If this property isn't present the supply is unlimited.",
      "minimum": 1,
      "maximum": 100_000_000_000.0
    },
    "b": {
      "title": "Backing",
      "description": "Specific amount of raw required to send NFT. Choosing a unique amount will make it easier to trace back it's history for non-full nodes."
      "type": "integer",
      "minimum": 1,
      "default": 1
    },
    "f": {
      "type": "integer",
      "description": "Issuer market fee per mille. Applied to raw during atomic swaps, sent directly to issuer.",
      "minimum": 0,
      "maximum": 190,
      "default": 0
    },
    "i": {
      "title": "IPFS CID as Uint8Array",
      "description": "For client to fetch NFT meta data unrelated to on-chain behaviour.",
      "type": "array",
      "items": {
        "type": "integer"
      },
      "minItems": 32,
      "maxItems": 32
    },
    "h": {
      "title": "Hyperdrive key as Uint8Array",
      "description": "For client to fetch NFT meta data unrelated to on-chain behaviour.",
      "type": "array",
      "items": {
        "type": "integer"
      },
      "minItems": 32,
      "maxItems": 32
    }
  }
}
```

### JSON Example

```
{
  "t": "Energy rich card",
  "b": 100000000000000000000001030307,
  "f": 19
}
```

The above JSON as msgpack hex (34 bytes):
```
83A174B0456E6572677920726963682063617264A162CB45F431E0FAE6D721A16613
```

Prepend the multi address header `CE14D51BA0` + `00` (40 bytes):
```
CE14D51BA00083A174B0456E6572677920726963682063617264A162CB45F431E0FAE6D721A16613
```

Split the hex into 64 char / 32 byte public keys and pad with zeros.
```
CE14D51BA00083A174B0456E6572677920726963682063617264A162CB45F431
E0FAE6D721A16613000000000000000000000000000000000000000000000000
```

Convert public keys into addresses.

Nano addresses:
```
nano_3mintnft1165n7td1jdgeos8gyb1gbnp8t31efiq6s73ed7ndx3ju1xqk197
nano_3r9twudk5ad84e11111111111111111111111111111111111111t39kgpxn
```

Banano addresses:
```
ban_3mintnft1165n7td1jdgeos8gyb1gbnp8t31efiq6s73ed7ndx3ju1xqk197
ban_3r9twudk5ad84e11111111111111111111111111111111111111t39kgpxn
```


## MonKey and natricon for NFT

The last block of the mint NFT commmand can be used as the identifying block for the NFT type. From the example above, the last block would be the block setting the `representative` field to `ban_3r9twudk5ad84e11111111111111111111111111111111111111t39kgpxn`.

Using the block hash as the NFT identifier prevents other accounts from minting the same NFT.

An NFT can be identified by NFT mint block hash, issuer, and token number.

MonKeys and natricons can be used for identifying the mint block hash and issuer at a glance.


## Token vanity

A vanity text name can be displayed instead of the token number.

Vanity text names are stored in the meta data.

