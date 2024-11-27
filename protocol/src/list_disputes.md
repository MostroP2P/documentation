# Listing Disputes

Mostro publishes new disputes with event kind `38383` and status `initiated`:

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

Clients can query this events by nostr event kind `38383`, nostr event author, dispute status (`s`), type (`z`)
