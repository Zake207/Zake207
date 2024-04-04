# Pasarela interior.

### RIP.
Trabaja con vectores de distancia, se basa en Bellman-Ford

PAQUETE RIP:
\[IP | UDP | MENSAJE RIP\]
udp funciona aquí en el puerto 520.

Existen 3 tipos:
+ v1: con clases
+ v2: sin clases
+ ng: IPv6

### OSPF.
Protocolo de estado de enlace, se basa en Dijkstra para hallar el camino mínimo entre routers.

PAQUETE OSPF
\[IP | MENSAJE OSPF\]
IP utiliza el protocolo 89

Existen 3 tipos:
+ v1: con clases
+ v2: sin clases
+ v3: IPv6

Tambien utiliza el método de inundación, sin embargo, es más escalable
# Pasarela exterior.
### BGP.
Permite obtener información sobre el alcance de las subredes, la función principal es conectar diferentes subredes con diferentes protocolos de enrutamiento para que puedan comunicarse sin problema.

PAQUETE BGP
\[IP | TCP | MENSAJE TCP\]

El grafo utilizado para calcular caminos tiene por nodos los sistemas autónomos conectados.

Para poder funcionar correctamente debe tener:
* Operación de adquisición de vecinos
* Actualización de vecinos alcanzables
* Detección de redes alcanzables.

Este protocolo no permite la actualización de los caminos mínimos en función del estado de la red, pues hay que establecer políticas de enrutamiento, pues no todo el mundo permitirá que se atraviese su red de forma gratuita (Ingeniería de trafico).