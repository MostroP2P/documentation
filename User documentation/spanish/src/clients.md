# Clientes. Cómo uso Mostro

Para utilizar Mostro, es necesario acceder a través de un cliente específico. A continuación, abordaremos varios de ellos, los cuales te permitirán interactuar tanto con Mostrod como con tu contraparte en una operación. 

Los clientes de Mostro disponibles hasta el momento son:
- **[Mostro web](./mostro-web.md)** (operativo): cliente con interfaz web.
- **[Mostro-cli](./mostro-cli.md)** (operativo): cliente desde línea de comandos.
- **[Mostrui](./mostrui.md)** (en desarrollo): cliente con interfaz TUI, que funciona en la terminal con una apariencia mejorada.
- **[Mostro mobile](./mostro-mobile.md)** (en desarrollo): aplicación móvil.

Cada cliente tiene características particulares, por lo que los usuarios pueden elegir cuál utilizar según sus intereses y cambiar entre ellos cuando lo consideren conveniente. Los clientes son los encargados de crear, almacenar y gestionar las claves de Nostr de sus usuarios. Para conocer cómo los clientes manejan la privacidad de los usuarios lee [aquí](./privacy.md).

Aunque algunos clientes ya están en funcionamiento, se encuentran en constante desarrollo, con la implementación de nuevas funciones, mejoras de UX, correción de errores, etc. Es posible que encuentres bugs; si esto sucede, por favor repórtalos, tu feedback es muy importante.

 **Nota:** Dos usuarios que utilicen diferentes clientes de Mostro pueden realizar un intercambio de Sats; sin embargo, para la comunicación directa entre ellos deben tene en cuenta qué tipo de mensajes aceptan sus respectivos clientes. Para ese tipo de comunicación, todos los clientes de Mostro deben utilizar mensajes cifrados con el algoritmo [NIP-44](https://github.com/nostr-protocol/nips/blob/master/44.md), pero si un cliente aun no lo ha implementado, sus usuarios no podrán visualizar mensajes enviados desde un cliente que sí lo tenga implementado. De forma similar pudiera ocurrir con otras funcionalidades, los desarrolladores de cada clientes hacen su mayor esfuerzo por actualizarlos lo antes posible.

Mostro es un proyecto FOSS, por lo que cualquier persona interesada puede crear un cliente para interactuar con este. Te invitamos a desarrollar tu propio cliente o a colaborar en el desarrollo de los ya existentes para mejorar la experiencia de los intercambios de Bitcoin P2P sin KYC en Nostr!

Para conocer más detalles sobre ellos continúa leyendo esta documentación.
