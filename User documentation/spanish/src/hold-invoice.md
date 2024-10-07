# Hold Invoices: Seguridad de los Intercambios en Mostro

Mostro utiliza hold invoices como mecanismo de escrow para asegurar los fondos de una operación, protegiendo al comprador contra posibles fraudes o impagos. A su vez, garantiza la seguridad del vendedor al no custodiar sus fondos directamente.

Para vender Sats a través de Mostro deberás pagar una hold invoice que este te proporcionará. Las hold invoices, o facturas retenidas, son un tipo de factura de Lightning Network que permiten el "bloqueo" en tu billetera de los Sats que vas a vender, pero que no se liquide el pago hasta que finalice la operación con tu contraparte. Dependiendo de la wallet que utilices, podrías ver tu pago como “en espera”, “congelado”, “en tránsito” o “pendiente”.

Una vez que el vendedor de Sats le indique a Mostro que ha recibido el fiat, se liquida automáticamente el pago de la hold invoice: los Sats se "desbloquean" y son cobrados por el nodo de Lightning Network del Mostro utilizado para el intercambio. Luego, se descontará el [fee](./fees-and-limits.md) correspondiente y se intentará pagar de inmediato la factura proporcionada por el comprador. Si el pago falla, Mostro solicitará una nueva factura al comprador y repetirá el proceso hasta que el pago se complete exitosamente.

Mostro minimiza el tiempo de custodia los fondos de los usuarios, limitándolo únicamente al periodo desde que se cobra la hold invoice al vendedor hasta que se paga al comprador, un proceso que puede tomar solo unos segundos.

El pago de la hold invoice también puede liquidarse si los usuarios entran en una [disputa](./disputes.md) y el administrador determina que los Sats deben ser transferidos al comprador. Por el contrario, si el administrador determina que la orden debe ser cancelada, el pago de la hold invoice se cancelará y los Sats se “desbloquearán” en la wallet del vendedor, sin haber salido nunca de ella. Esto también ocurrirá si se realiza una [cancelación](./cancelling-an-order.md) cooperativa, o si se excede el tiempo de validez de la hold invoice, que es limitado. 

Las hold invoices generadas por el nodo de Lightning Network del Mostro actualmente activo en mainnet (`npub1ykvsmrmw2hk7jgxgy64zr8tfkx4nnjhq9eyfxdlg3caha3ph0skq6jr3z0`) tienen  un tiempo de validez aproximado de 24 horas.
