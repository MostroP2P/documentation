# Other events published by Mostro

Each Mostro instance periodically publishes events with relevant information about its status, such as the code version it is using, the latest commit, the fees it charges, allowed exchange limits, the relays it publishes to, and much more. Below, we provide details on these events.

## Mostro Instance Status
This event contains specific data about a Mostro instance. The instance is identified by the label `mostro_pubkey`.
```json
[
  "EVENT",
  "RAND",
  {
    "tags": [
      ["d", "info-25990d8f6e55ede920c826aa219d69b1ab39cae02e489337e88e3b7ec4377c2c"],
      ["mostro_pubkey", "25990d8f6e55ede920c826aa219d69b1ab39cae02e489337e88e3b7ec4377c2c"],
      ["mostro_version", "0.12.8"],
      ["mostro_commit_id", "69052b2adba6c006e6929afda27f041a427f58f8"],
      ["max_order_amount", "20000"],
      ["min_order_amount", "100"],
      ["expiration_hours", "24"],
      ["expiration_seconds", "900"],
      ["fee", "0.006"],
      ["pow", "0"],
      ["hold_invoice_expiration_window", "900"],
      ["hold_invoice_cltv_delta", "298"],
      ["invoice_expiration_window", "900"],
      ["y", "mostrop2p"],
      ["z", "info"]
    ],
    "content": "",
    "sig": "db3591d04508db3e5f6ec45ca5c65d6309f7815842d0f166c612cd17f3885deeea1649e6865c301012664ed6631e58bd4e2090712b94aa79a2b571265e3dcb03",
    "id": "52556bcd6100131d7918a75d0dd47d39c60ff74ce5045f182f4ace3a1b9e70f1",
    "pubkey": "25990d8f6e55ede920c826aa219d69b1ab39cae02e489337e88e3b7ec4377c2c",
    "created_at": 1731701441,
    "kind": 38383
  }
]
```
Below is an explanation of the meaning of some of the labels in this event, all of which can be modified by anyone running a Mostro instance.

- `mostro_version`: The version of the Mostro daemon running on the instance.
- `mostro_commit_id`: The ID of the last commit used by the instance.
- `max_order_amount`: The maximum amount of Satoshis allowed for exchange.
- `min_order_amount`: The minimum amount of Satoshis allowed for exchange.
- `expiration_hours`: The maximum time, in hours, that an order can remain in `pending` status before it expires.
- `expiration_seconds`: The maximum time, in seconds, that an order can remain in `waiting-payment` or `waiting-buyer-invoice` status before being canceled or reverted to `pending` status.
- `fee`: The fee percentage charged by the instance. For example, "0.006" means a 0.6% fee.
- `pow`: The Proof of Work required of incoming events.
- `hold_invoice_expiration_window`: The maximum time, in seconds, for the hold invoice issued by Mostro to be paid by the seller.
- `hold_invoice_cltv_delta`: The number of blocks in which the Mostro hold invoice will expire.
- `invoice_expiration_window`: The maximum time, in seconds, for a buyer to submit an invoice to Mostro.

## Information about the Relays Where Events Are Published

The operator of a Mostro instance decides which relays the events from that instance are published to. This information can be accessed in events [kind 10002](https://github.com/nostr-protocol/nips/blob/master/65.md), which are published by the Mostro instances.

```json
[
  "EVENT",
  "RAND",
  {
    "tags": [
      [
        "r",
        "wss://relay.mostro.network/"
      ],
      [
        "r",
        "wss://nostr.bilthon.dev/"
      ]
    ],
    "content": "",
    "sig": "e48c14009871300e92ba66d6d37552c46c8259bf5efa2ef91874e9377cabf849987e9f785f7b8e4a740b691bb76111999d6ef4e703c8765214a7771f8e38e560",
    "id": "7a31879cbb4f32b86ca535912ba568722c52845e1517468249b66f9af6eff05c",
    "pubkey": "25990d8f6e55ede920c826aa219d69b1ab39cae02e489337e88e3b7ec4377c2c",
    "created_at": 1731680102,
    "kind": 10002
  }
]
```
The `r` label indicates the relays through which the Mostro instance is publishing its events.