# Dispute

A use can start a dispute in an order with status `active` or `fiat-sent` sending action `dispute`, here is an example where the seller initiates a dispute:

```json
{
  "order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "action": "dispute",
    "payload": null
  }
}
```

## Mostro response

Mostro will send this message to the seller:

```json
{
  "order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "action": "dispute-initiated-by-you",
    "payload": {
      "dispute": "efc75871-2568-40b9-a6ee-c382d4d6de01"
    }
  }
}
```

And here is the message to the buyer:

```json
{
  "order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "action": "dispute-initiated-by-peer",
    "payload": {
      "dispute": "efc75871-2568-40b9-a6ee-c382d4d6de01"
    }
  }
}
```

Mostro will not update the addressable event with `d` tag `ede61c96-4c13-4519-bf3a-dcf7f1e9d842` to change the status to `dispute`, this is because the order is still active, the dispute is just a way to let the admins and the other party know that there is a problem with the order.

## Mostro send a addressable event to show the dispute

Here is an example of the event sent by Mostro:

```json
[
  "EVENT",
  "RAND",
  {
    "id": "<Event id>",
    "pubkey": "<Mostro's pubkey>",
    "created_at": 1703016565,
    "kind": 38383,
    "tags": [
      ["d", "efc75871-2568-40b9-a6ee-c382d4d6de01"],
      ["s", "initiated"],
      ["y", "mostrop2p"],
      ["z", "dispute"]
    ],
    "content": "",
    "sig": "<Mostro's signature>"
  }
]
```

Mostro admin will see the dispute and can take it using the dispute `Id` from `d` tag, in this case `efc75871-2568-40b9-a6ee-c382d4d6de01`.

```json
{
  "dispute": {
    "version": 1,
    "id": "efc75871-2568-40b9-a6ee-c382d4d6de01",
    "action": "admin-take-dispute",
    "payload": null
  }
}
```

Mostro will send a confirmation message to the admin with the order details:

```json
{
  "dispute": {
    "version": 1,
    "id": "efc75871-2568-40b9-a6ee-c382d4d6de01",
    "action": "admin-took-dispute",
    "payload": {
      "order": {
        "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
        "kind": "sell",
        "status": "active",
        "amount": 7851,
        "fiat_code": "VES",
        "fiat_amount": 100,
        "payment_method": "face to face",
        "premium": 1,
        "master_buyer_pubkey": "<Buyer's trade pubkey>",
        "master_seller_pubkey": "<Seller's trade pubkey>",
        "buyer_invoice": "lnbcrt11020n1pjcypj3pp58m3d9gcu4cc8l3jgkpfn7zhqv2jfw7p3t6z3tq2nmk9cjqam2c3sdqqcqzzsxqyz5vqsp5mew44wzjs0a58d9sfpkrdpyrytswna6gftlfrv8xghkc6fexu6sq9qyyssqnwfkqdxm66lxjv8z68ysaf0fmm50ztvv773jzuyf8a5tat3lnhks6468ngpv3lk5m7yr7vsg97jh6artva5qhd95vafqhxupyuawmrcqnthl9y",
        "created_at": 1698870173
      }
    }
  }
}
```

Also Mostro will broadcast a new addressable dispute event to update the dispute `status` to `in-progress`:

```json
[
  "EVENT",
  "RAND",
  {
    "id": "<Event id>",
    "pubkey": "<Mostro's pubkey>",
    "created_at": 1703020540,
    "kind": 38383,
    "tags": [
      ["d", "efc75871-2568-40b9-a6ee-c382d4d6de01"],
      ["s", "in-progress"],
      ["y", "mostrop2p"],
      ["z", "dispute"]
    ],
    "content": "",
    "sig": "<Mostro's signature>"
  }
]
```
