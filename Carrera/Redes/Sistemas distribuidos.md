Pueden ser del tipo cliente-servidor o Peer-to-peer
+ Cliente-servidor: Existe un host activo que provee servicios a los clientes. Requiere arquitectura intensiva
+ Peer to peer: Servicios no centralizados, arquitectura auto-escalable, se explota la comunicación entre los hosts
## Comunicación de mensajes.
Para direccionar procesos se debe conocer la dirección del host y del proceso (IP y puerto).
La organización IANA se encarga de gestionar los nombres de dominios, recursos y asignaciones de protocolos

Se utiliza una caché web para ahorrar tiempo de conexión, para ello se usan los servidores proxy como almacenamiento intermedio.

HTTP no cuenta con memoria de conexión, para que puedan tener esto se usan las cookies.

DNS Es una base de datos distribuida que traduce las direcciones IP en nombres legibles. Un host puede tener diferentes alias y un alias puede pertenecer a diferentes hosts. Hay 3 tipos de servidores:
+ Servidor raiz
+ Servidor de dominio de nivel superior
+ Servidor autoritativo

Además existe el Servidor DNS local empleado para acelerar consultas a nivel local