# Exchange Times

Mostro is designed for bitcoin-to-fiat exchanges to be fast, so it is recommended to use instant fiat payment methods.

Each Mostro instance operator can set their own time frames for each step of the exchange, fostering competition among Mostro instances and allowing users to select the one that best fits their needs.

Below are the specific time frames for the Mostro instance currently active on mainnet (`npub1ykvsmrmw2hk7jgxgy64zr8tfkx4nnjhq9eyfxdlg3caha3ph0skq6jr3z0`). As more Mostro instances become available, this information should be accessible to users so they can choose their preferred one.

When an offer is posted, it remains in the order book for *23 hours*. If no one takes it within that time, it will be automatically deleted.

Once someone takes an offer, they have up to *15 minutes* to either pay the hold invoice if they are the seller or provide an invoice if they are the buyer. If they do not complete their part within that time frame, the order will be automatically reposted. However, if they do, then the counterparty will have up to *15 minutes* to complete their corresponding action (either paying the hold invoice or providing an invoice, depending on their role in the exchange); if they fail to do so, the order will be canceled and not reposted.

After the seller pays the hold invoice and the buyer provides their invoice, they have until the expiration of the [hold invoice](./hold-invoice.md) provided by Mostro to finalize the exchange. For the Mostro instance `npub1ykvsmrmw2hk7jgxgy64zr8tfkx4nnjhq9eyfxdlg3caha3ph0skq6jr3z0`, this period is approximately *24 hours*. During this time, the buyer must send the fiat payment, and the seller must release the sats upon confirming receipt of the fiat. If this time frame is exceeded, the order will expire, and the sats will be returned to the original wallet without Mostro being able to intervene. For this reason, it is recommended to only use instant fiat payment methods.

Within this validity period, users can successfully complete the exchange, [cancel it](./cancelling-an-order.md) cooperatively, or open a [dispute](./disputes.md). After the [hold invoice](./hold-invoice.md) expires, Mostro has no ability to intervene in that order.

If both participants in a transaction are online and use instant fiat payment methods, the transactions can be completed almost instantly.
