# Send and Receive Assets

## `send#asset` block

A send block with the `representative` field set to `asset_representative`.


### `send#burn` block

A `send#asset` block where the recipient is one of the burn accounts:

```
ban_1burnbabyburndiscoinferno111111111111111111111111111aj49sw3w
ban_1uo1cano1bot1a1pha1616161616161616161616161616161616p3s5tifp
ban_1ban116su1fur16uo1cano16su1fur16161616161616161616166a1sf7xw
ban_1111111111111111111111111111111111111111111111111111hifc8npp
```


## `receive#asset`

Any receive block for `send#asset`

### Validation

`receive#asset` must not be confirmed at a lower block height than `send#asset` in an account for `send#asset` to be valid.

`send#asset` to self (link set to sender account in Banano block) must be received, denoted as `receive#asset`, before any other action is allowed such as `send#asset`, `send#atomic_swap`, or `send#atomic_swap_delegation`.
