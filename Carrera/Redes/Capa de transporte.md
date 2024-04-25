La encargada de la comunicación lógica.
Sus protocolos son TCP y UDP.

# Técnicas de transferencia fiable
Las siguientes técnicas están basadas en el envío de paquetes de confirmación para poder controlar el envío de paquetes.

Se implementan unos temporizadores para detectar la pérdida de estos paquetes y poder actuar de manera consecuente.

Cada paquete tiene un número de confirmación y de secuencia que permite ordenar los paquetes de datos en el destinatario.

La eficiencia de los siguientes métodos se mide con:
E = Te/(Te + RTT)
##### Parada y espera.
Se basa en mandar un paquete y esperar a recibir la confirmación para mandar el siguiente.
##### Vuelta atrás N
Mandas un número de paquetes seguidos si tener que esperar la respuesta del destinatario para aumentar la eficiencia.

# /// FALTA CONTENIDO INTERMEDIO

# TCP
Protocolo orientado a conexión que consta de 3 fases:
+ Inicio de conexión
+ Envío/Recepción
+ Cierre de conexión
Utiliza un número de secuencia en su cabecera para ordenar los ficheros y asegurar las entregas.

El número de confirmaciones en TCP es el siguiente byte que espera recibir el receptor. El numero de secuencia es el numero del byte que se envía, es decir, si hacen envíos de 4 bytes los numeros de secuencia serán 0, 4, 8, ...

Sigue el principio de confirmación acumulativa, esto es, una confirmación con un numero de aceptación X, confirma todos los anteriores.

Se utilizan temporizadores para detectar un paquete perdido y poder reenviarlo. El tiempo de espera varía dependiendo de a qué se está conectando. Este se establece midiendo el tiempo del envío del primer paquete y se va estimando a lo largo de la conexión. Es necesario que el receptor sea capaz de detectar duplicados para no ocasionar problemas cuando se pierdan paquetes.

También se puede duplicar el temporizador cuando, tras perder un paquete, se hace el reenvío para darle tiempo de recibir la confirmación. Esto proporciona un control de congestión limitado.

La retransmisión rápida consiste en hacer varios envíos sin llegar a esperar el ACK, si se detecta una perdida pues se lleva un control de los ACK recibidos se hace inmediatamente el reenvío del paquete, incluso antes de que acabe el temporizador.

El control de flujo consiste en adaptar la velocidad de emisión de paquetes del emisor a la velocidad de procesamiento del receptor. Se da entre cualquier par de entidades conectadas.

Utiliza una ventana de recepción para calcular los bytes que se enviarán, por lo que si la ventana es de 0, cuando esto pasa se comienzan a enviar mensajes de 1 byte para forzar las confirmaciones y actualizar el la ventana de recepción. Se utiliza el algoritmo de Nagle.

Para evitar el síndrome de la ventana tonta se debe esperar hasta que haya suficiente espacio en el buffer.

## Control de congestión
Cada emisor debe controlar su velocidad de transmisión en función de la congestión de la red
==Pregunta de examen: Diferencias entre control de flujo y control de congestión==

Se crea la ventana de congestión limitar la velocidad del emisor, esta varia en función de las transmisiones, en caso de perdidas se baja la velocidad general, si todo va bien se aumenta.

El control de congestión tiene tres algoritmos principales que derivan en diferentes tipos de TCP: Arranque lento (crece la ventana exponencialmente), evitación de congestión(crece la ventana de unidad en unidad) y la recuperación rápida (al detectar 3 ACK's duplicados reduce el umbral y la ventana a la mitad)