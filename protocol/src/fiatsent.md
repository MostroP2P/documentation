# Fiat sent

After the buyer sends the fiat money to the seller, the buyer should send a message in a Gift wrap Nostr event to Mostro indicating that the fiat money was sent, the rumor's content would look like this:

```json
{
  "order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "action": "fiat-sent",
    "payload": null
  }
}
```

The event to send to Mostro would look like this:

```json
{
  "id": "<Event id>",
  "kind": 1059,
  "pubkey": "<Ephemeral pubkey>",
  "content": "<sealed-rumor-content>",
  "tags": [["p", "Mostro's pubkey"]],
  "created_at": 1234567890,
  "sig": "<Signature of ephemeral pubkey>"
}
```

## Mostro response

Mostro send messages to both parties confirming `fiat-sent` action and sending again the counterpart pubkey, here an example of the message to the buyer:

```json
{
  "order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "action": "fiat-sent-ok",
    "payload": {
      "Peer": {
        "pubkey": "<Seller's trade pubkey>"
      }
    }
  }
}
```

And here an example of the message from Mostro to the seller:

```json
{
  "order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "pubkey": "<Seller's trade pubkey>",
    "action": "fiat-sent-ok",
    "payload": {
      "Peer": {
        "pubkey": "<Buyer's trade pubkey>"
      }
    }
  }
}
```

Mostro updates the addressable event with `d` tag `ede61c96-4c13-4519-bf3a-dcf7f1e9d842` to change the status to `fiat-sent`:

```json
[
  "EVENT",
  "RAND",
  {
    "id": "<Event id>",
    "pubkey": "<Mostro's pubkey>",
    "created_at": 1702549437,
    "kind": 38383,
    "tags": [
      ["d", "ede61c96-4c13-4519-bf3a-dcf7f1e9d842"],
      ["k", "sell"],
      ["f", "VES"],
      ["s", "fiat-sent"],
      ["amt", "7851"],
      ["fa", "100"],
      ["pm", "face to face"],
      ["premium", "1"],
      ["network", "mainnet"],
      ["layer", "lightning"],
      ["expiration", "1719391096"],
      ["y", "mostrop2p"],
      ["z", "order"]
    ],
    "content": "",
    "sig": "<Mostro's signature>"
  }
]
```
