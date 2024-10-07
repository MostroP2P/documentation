# Tiempo de Intercambio

Mostro está diseñado para que los intercambios de bitcoin por monedas fiat sean rápidos, por lo que se recomienda utilizar métodos de pago fiat instantáneos.

Cada operador de una instancia de Mostro puede establecer sus plazos de tiempo para cada etapa del intercambio, lo que fomenta la competencia entre Mostros y permite a los usuarios seleccionar el que mejor se ajuste a sus necesidades.

A continuación, se detallan los diferentes plazos de la instancia de Mostro actualmente activa en mainnet (`npub1ykvsmrmw2hk7jgxgy64zr8tfkx4nnjhq9eyfxdlg3caha3ph0skq6jr3z0`). A medida que existan más instancias de Mostro, esta información deberá ser accesible a los usuarios para que puedan elegir la que prefieran.

Al publicar una oferta, esta permanece en el libro de órdenes hasta *23 horas*. Si nadie la toma durante ese tiempo, se eliminará automáticamente.

Una vez que alguien toma una oferta tiene hasta *15 minutos* para pagar la hold invoice si es el vendedor, o proporcionar una invoice si es el comprador. Si no cumple con su parte en ese tiempo, la orden se volverá a publicar automáticamente. Pero si cumple, luego la contraparte tendrá hasta *15 minutos* para para completar su acción correspondiente (pagar la hold invoice o proporcionar una factura, según su rol en el intercambio) si este no lo hace, la orden será cancelada y no se republicará.

Después de que el vendedor paga la hold invoice y el comprador proporciona su factura, tienen de tiempo para concretar el intercambio hasta que expire la [hold invoice](./hold-invoice.md) que Mostro le proporcionó al vendedor. En la instancia de Mostro `npub1ykvsmrmw2hk7jgxgy64zr8tfkx4nnjhq9eyfxdlg3caha3ph0skq6jr3z0` este plazo es de *24 horas* aproximadamente. Durante este tiempo, el comprador debe enviar el pago en fiat y el vendedor liberar los Sats al confirmar la recepción del fiat. Si se excede ese plazo, la orden expirará y los Sats serán devueltos a la wallet de origen sin que Mostro pueda hacer nada al respecto. Por esta razón, se recomienda utilizar únicamente métodos de pago fiat instantáneos.

Dentro de este período de validez, los usuarios pueden finalizar satisfactoriamente el intercambio, [cancelarlo](./cancelling-an-order.md) cooperativamene, o abrir una [disputa](./disputes.md). Luego de que la [hold invoice](./hold-invoice.md) expire, Mostro no tiene capacidad de intervenir en esa orden.

Si ambos participantes de una operación están en línea y utilzan métodos de pago del fiat inmediatos, las transacciones pueden completarse de forma casi instantánea.
