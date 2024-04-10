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