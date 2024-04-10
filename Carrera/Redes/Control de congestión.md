La congestión se da cuando se el número de paquetes se aproxima a la capacidad de gestión de la red, produciendo colas y provocando la pérdida de paquetes.

En toda red a medida que se aumenta la carga se aumenta el rendimiento hasta cierto punto en que ya empieza a congestionarse![[Pasted image 20240404115115.png]]
\> <
 3

A la hora de hacer los rechazos existen varios criterios.
+ Equidad: trata de descartarse el mismo número de paquetes de todas las conexiones.
+ Calidad de servicios: Los flujos se tratan de cierta manera para optimizar el rendimiento de las aplicaciones.
+ Reservas: Ser pre-establecen ciertos parámetros de calidad de servicios antes de conectarse, si la red no puede asegurar estos parámetros no permite la conexión
### Métodos de control.
##### Señalización implícita.
Se detecta al ver que hay una pérdida de paquetes en las comunicaciones, o cuando aumenta el retardo considerablemente.

Es responsabilidad de los sistemas terminales(nodos emisores) gestionar la congestión, se basa en TCP
##### Señalización explicita.
Se envían paquetes para notificar el estado de la red
Utiliza la técnica de choque.

Se puede hacer hacia delante o hacia detrás
![[Pasted image 20240408111705.png]]
La señalización de la congestión puede ser:
+ Binaria
+ Basada en crédito
+ Basada en velocidad
