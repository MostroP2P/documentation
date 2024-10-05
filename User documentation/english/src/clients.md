# Clients. How to use Mostro

To use Mostro, you need to access it through a specific client. Below, we will cover several of them, which will allow you to interact both with Mostrod and with your counterpart in an operation.

The available Mostro clients so far are:
- **[Mostro web](./mostro-web.md)** (operational): web interface client.
- **[Mostro-cli](./mostro-cli.md)** (operational): command line client.
- **[Mostrui](./mostrui.md)** (in development): TUI client, which operates in the terminal with an enhanced appearance.
- **[Mostro mobile](./mostro-mobile.md)** (in development): mobile application.

Each client has particular features, so users can choose which one to use based on their preferences and switch between them as they see fit. The clients are responsible for creating, storing, and managing their users' Nostr keys. To learn how clients handle user privacy, read [here](./privacy.md).

Although some clients are already operational, they are under constant development, with new features being implemented, UX improvements, bug fixes, etc. You may encounter bugs; if this happens, please report them, your feedback is very important.

**Note:** Two users using different Mostro clients can exchange sats; however, for direct communication between them, they should consider what type of messages their respective clients accept. For this type of communication, all Mostro clients must use messages encrypted with the [NIP-44](https://github.com/nostr-protocol/nips/blob/master/44.md) algorithm. However, if a client has not yet implemented it, its users will not be able to view messages sent from a client that has. A similar situation may occur with other functionalities. Developers of each client make their best effort to update them as soon as possible.

Mostro is a FOSS project, so anyone interested can create a client to interact with it. We encourage you to develop your own client or collaborate on the development of existing ones to enhance the experience of P2P Bitcoin exchanges without KYC on Nostr!

To learn more details about them, keep reading this documentation.
