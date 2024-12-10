## Overview

In order to have a shared order's book, Mostro daemon send [Addressable Events](https://github.com/nostr-protocol/nips/blob/master/01.md#kinds) with `38383` as event `kind`, you can find more details about that specific event [here](./order-event.md)

## Communication between users and Mostro

All messages from/to Mostro should be [Gift wrap Nostr events](https://github.com/nostr-protocol/nips/blob/master/59.md), the `content` of the `rumor` event should be a nip44 encrypted JSON-serialized string (with no white space or line breaks) of the following structure:

- [Wrapper](https://docs.rs/mostro-core/latest/mostro_core/message/enum.Message.html): Wrapper of the message
  - `version`: Version of the protocol, currently `1`
  - `id`: (optional) Wrapper Id
  - `request_id`: (optional) Mostro daemon should send back this same id in the response
  - `trade_index`: (optional) This field is used by users who wants to maintain reputation, it should be the index of the trade in the user's trade history
  - [action](https://docs.rs/mostro-core/latest/mostro_core/message/enum.Action.html): Action to be performed by Mostro daemon
  - [payload](https://docs.rs/mostro-core/latest/mostro_core/message/enum.Content.html) (optional): Payload of the message, this field is optional and depends on the action

These fields are relative to the wrapper, here an example of a `fiat-sent` Order message, in this case `id` is the Order Id:

```json
{
  "order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "request_id": "12345",
    "trade_index": 1,
    "action": "fiat-sent",
    "payload": null
  }
}
```
