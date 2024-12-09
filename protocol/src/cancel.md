# Cancel Order

A user can cancel an order created by himself and with status `pending` sending action `cancel`, the rumor's content of the message will look like this:

```json
{
  "order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "action": "cancel",
    "payload": null
  }
}
```

## Mostro response

Mostro will send a message with action `cancel` confirming the order was canceled, here an example of rumor's content of the message:

```json
{
  "order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "action": "canceled",
    "payload": null
  }
}
```

Mostro updates the parameterized replaceable event with `d` tag `ede61c96-4c13-4519-bf3a-dcf7f1e9d842` to change the status to `canceled`:

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
      ["s", "canceled"],
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

## Cancel cooperatively

A user can cancel an `active` order, but will need the counterparty to agree, let's look at an example where the seller initiates a cooperative cancellation:

```json
{
  "order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "action": "cancel",
    "payload": null
  }
}
```

Mostro will send this message to the seller:

```json
{
  "order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "action": "cooperative-cancel-initiated-by-you",
    "payload": null
  }
}
```

And this message to the buyer:

```json
{
  "order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "action": "cooperative-cancel-initiated-by-peer",
    "payload": null
  }
}
```

Mostro updates the parameterized replaceable event with `d` tag `ede61c96-4c13-4519-bf3a-dcf7f1e9d842` to change the status to `cooperatively-canceled`:

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
      ["s", "cooperatively-canceled"],
      ["amt", "7851"],
      ["fa", "100"],
      ["pm", "face to face"],
      ["premium", "1"],
      ["y", "mostrop2p"],
      ["z", "order"]
    ],
    "content": "",
    "sig": "<Mostro's signature>"
  }
]
```

The buyer can accept the cooperative cancellation sending this message:

```json
{
  "order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "action": "cancel",
    "payload": null
  }
}
```

And Mostro will send this message to both parties:

```json
{
  "order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "action": "cooperative-cancel-accepted",
    "payload": null
  }
}
```
