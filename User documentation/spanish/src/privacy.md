# Privacidad en Mostro

La comunicación entre Mostrod y los usuarios se realiza través de los [clientes de Mostro](./clients.md) mediante mensajes [NIP-59](https://github.com/nostr-protocol/nips/blob/master/59.md). Estos mensajes tienen su contenido y la clave pública del emisor cifrados y "envueltos" por una clave efímera, lo que evita que se revele públicamente la identidad de quien interactúa con Mostro. Para aumentar la privacidad, los [clientes de Mostro](./clients.md) deben generar automáticamente una nueva clave privada a los usuarios para cada orden que tomen o creen. Así, cuando Mostro envíe mensajes [NIP-59](https://github.com/nostr-protocol/nips/blob/master/59.md) a los usuarios, el evento generado mostrará una clave pública que será usada únicamente para esa operación, garantizando una nueva identidad para cada intercambio e impidiendo que las transacciones de compra y venta puedan ser asociadas a una sola persona.

Los [clientes de Mostro](./clients.md) no compartirán las claves privadas de los usuarios con una instancia de Mostro, y por consiguiente con su administrador, en ningún caso.

La comunicación entre el comprador y el vendedor durante una operación, se realiza de cliente a cliente, mediante mensajes cifrados con el algoritmo [NIP-44](https://github.com/nostr-protocol/nips/blob/master/44.md) que, aunque revela las claves públicas que se están comunicando, en cada operación los usuarios siempre deben usar una nueva identidad de Nostr, lo que garantiza su privacidad. Además, estos mensajes no se envían a Mostrod, por lo que no tiene acceso ni recopila información personal de los usuarios. 

Además, [NIP-44](https://github.com/nostr-protocol/nips/blob/master/44.md) permite que el cliente cree una *conversation key* asociada al par de claves de los dos usuarios involucrados en una operación y a la que solo ellos tienen acceso. Dicha *conversation key* tiene una copia de la conversación entre ambos usuarios, y en caso de [disputa](./disputes.md), si los usuarios lo desean pueden entregársela al administrador que los atienda, como evidencia de los hechos.


