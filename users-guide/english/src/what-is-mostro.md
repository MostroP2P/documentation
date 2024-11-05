# What is Mostro?

Mostro is a peer-to-peer (P2P) bitcoin exchange platform on the Lightning Network for any local currency, operating on the [Nostr](https://nostr.com/) protocol and not requiring Know Your Customer (KYC) procedures.

It uses [hold invoices](./hold-invoice.md) as an escrow system to provide security for the exchange of sats, minimizing custody and reducing the trust needed in both the counterparty and Mostro.

By operating on [Nostr](https://nostr.com/), a communication protocol designed to be censorship-resistant due to the decentralization of its infrastructure, Mostro ensures that it is very difficult to block bitcoin exchanges, censor the posting of buy and sell offers, or hinder communication between users involved in an exchange. Additionally, as more [Mostro instances](https://github.com/MostroP2P/mostro) become active, combined with Nostr's inherent decentralization, it will become increasingly difficult to stop P2P bitcoin exchanges without KYC.

## Origin of Mostro

Mostro is inspired by [@lnp2pBot](https://github.com/lnp2pBot/bot), a Telegram bot created in 2021 to facilitate bitcoin exchange via the Lightning Network without surrendering personal data, without custody of funds, and without KYC. The bot has grown steadily and organically, with global reach and a particularly significant impact in Latin America, where the population faces financial challenges and finds an alternative in bitcoin. It has also gained popularity in countries under authoritarian regimes, such as Cuba and Venezuela, where people use bitcoin to resist tyranny and reduce their dependence on local currency.

Although the [@lnp2pBot](https://github.com/lnp2pBot/bot) operates efficiently, it functions on Telegram, a platform that, while offering many advantages, could potentially come under pressure from powerful governments seeking to pursue political dissidents or inconvenient public figures. In this context, [Nostr](https://nostr.com/) emerges as an ideal alternative, allowing an exchange system like Mostro to operate without the risk of censorship by powerful entities, thus ensuring greater privacy and security for users.
