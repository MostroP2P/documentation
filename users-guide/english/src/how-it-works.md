# How does Mostro work?

To understand how Mostro works, it is important to know its components:

- [Mostro daemon (Mostrod)](https://github.com/MostroP2P/mostro): Manages communication between users and the Lightning Network (LN) node. It publishes Nostr events, executes actions sent by users, and guides them through the exchange process. 

- Lightning Network node associated with the Mostrod instance: Creates and manages the [hold invoices](./hold-invoice.md) that sellers must pay and makes payments for the invoices provided by buyers.

- [Mostro clients](./clients.md): These are the applications that users interact with directly. They provide the communication interface between Mostrod and the users. The clients send Mostrod the actions performed by users, such as creating an order, opening a dispute, releasing sats, among others. They are also responsible for generating and handling users' private keys.

The following diagram summarizes how Mostrod, the seller (via a Mostro client), and the LN node interact:  
![order-flow](./assets/images/order-flow.png)

## Bitcoin Sale Flow on Mostro

- **Seller:** Alice  
- **Buyer:** Bob

1. **Order creation:**  
   Alice accesses a [Mostro client](./clients.md) and decides to post an order to sell 5000 sats for 3 USD, to receive payment on her XYZ card. The interface for creating the order will depend on the [client](./clients.md) she uses. The order is posted in an order book that can be accessed from any Mostro client. If another user does not take the order within [24 hours](times.md), it will be automatically deleted.

2. **Order taken by the buyer:**  
   Bob, interested in buying sats, accesses a [Mostro client](./clients.md) (not necessarily the same one Alice used). He finds the offer of 5000 sats for 3 USD and decides to take it. He is then asked to provide an invoice for 5000 sats within [15 minutes](times.md). Bob generates the invoice in his LN wallet and sends it to Mostro, who instructs him to wait [15 minutes](times.md) for his counterparty to respond.

3. **Payment and communication between parties:**  
   Alice receives a message from Mostro notifying her that someone has taken her offer and that she must pay a [hold invoice](./hold-invoice.md) for 5000 sats within [15 minutes](times.md). If she does not make the payment, the order will be canceled. Once Alice pays the invoice, Mostro reveals Bob’s public key to Alice and vice versa, allowing them to start a private chat. At this point, Alice must provide Bob with the number of her XYZ card to receive the fiat payment. When Bob sends her the 3 USD, he presses the *fiat sent* button in his Mostro client. Alice receives a notification to verify receipt of the fiat and then release the sats to Bob.

4. **Sats release:**  
   When Alice confirms she received the 3 USD, she presses the *release* button in her Mostro client. Then Mostro will collect the 5000 sats from Alice's wallet and pay Bob's invoice. Finally, Mostro will ask both parties to rate their counterparty.
   
When Mostro connects both users, the time they have to complete the exchange is limited by the duration of the [hold invoice](./hold-invoice.md) provided by the Mostro instance they are using. Users must respect this time frame; for more information, see [here](times.md).  

If during the process, Alice and Bob decide not to proceed with the exchange, they can [cancel](./cancelling-an-order.md) the order cooperatively. If either party attempts to cancel arbitrarily or defraud the other, the other party can open a [dispute](./disputes.md).

> **Note:** In this example, it is assumed that Mostro’s fees are 0. For more information on fees, see [Exchange Fees and Limits](./fees-and-limits.md).

### Technical Explanation

1. **Alice creates the order:**  
  When Alice creates the sale offer, her Mostro client should automatically generate a new Nostr private key that Alice will use only for that order (a new private key should always be generated for each order to protect users’ [privacy](./privacy.md)). Using that key, Alice sends a [NIP-59](https://github.com/nostr-protocol/nips/blob/master/59.md) message to Mostrod with the order details. Then, Mostrod publishes an [addressable event](https://github.com/nostr-protocol/nips/blob/master/01.md#kinds) of type 38383, with the order details and its status: `pending`. Mostro clients monitor these events and display those orders with `pending` status in their order books.

2. **Bob takes the order:**  
   When Bob takes the order, his Mostro client automatically generates a new Nostr private key for this order, then sends a [NIP-59](https://github.com/nostr-protocol/nips/blob/master/59.md) message to Mostrod indicating that he has taken that offer. Mostrod publishes a new event 38383 for that order, this time with the status `waiting-buyer-invoice`, which removes the order from all clients' order books as it is no longer `pending`. Mostrod sends Bob a [NIP-59](https://github.com/nostr-protocol/nips/blob/master/59.md) message requesting an invoice for 5000 sats. Bob sends the invoice to Mostrod in a [NIP-59](https://github.com/nostr-protocol/nips/blob/master/59.md) message, and then Mostrod publishes an event 38383 for that order, this time with the status `waiting-payment`.

3. **Alice pays the hold invoice:**  
   Mostrod sends Alice a [NIP-59](https://github.com/nostr-protocol/nips/blob/master/59.md) message with the [hold invoice](./hold-invoice.md) generated by the associated LN node. If Alice pays within the 15 minutes, Mostro sends her a [NIP-59](https://github.com/nostr-protocol/nips/blob/master/59.md) message revealing Bob's pubkey, and another message to Bob revealing Alice's pubkey. Additionally, it updates the event 38383 for this order with the status `active`. Now, Alice and Bob can communicate directly through encrypted messages using the [NIP-44](https://github.com/nostr-protocol/nips/blob/master/44.md) algorithm, and Mostrod does not receive any of those messages. When Bob makes the fiat payment and presses *fiat sent* in his client, he sends a [NIP-59](https://github.com/nostr-protocol/nips/blob/master/59.md) message with the `fiat-sent` action to Mostrod, who in turn sends a [NIP-59](https://github.com/nostr-protocol/nips/blob/master/59.md) message to Alice with that same action, and her client displays a *release* button to release the sats if she has received the payment. Mostrod also publishes an event 38383 for that order with the status `fiat-sent`.
   
4. **Alice releases the sats:**  
   When Alice presses the *release* button in her client, she sends a [NIP-59](https://github.com/nostr-protocol/nips/blob/master/59.md) message to Mostrod indicating that the sats should be released to Bob. Then, the LN node associated with that instance of Mostrod settles the payment of the [hold invoice](./hold-invoice.md) and pays the invoice provided by Bob. At the end of the process, Mostrod publishes an event 38383 for that order with the status `success` and sends a [NIP-59](https://github.com/nostr-protocol/nips/blob/master/59.md) message to Alice and Bob, requesting that they rate their counterparty, who send back their rating through a [NIP-59](https://github.com/nostr-protocol/nips/blob/master/59.md) message.
   
For more details on the communication between Mostrod and its clients, you can read [here](https://mostro.network/messages).
