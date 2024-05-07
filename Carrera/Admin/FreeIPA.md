Gestiona los usuarios y máquinas de una entidad, también establece políticas para operar con los servicios e información.

Para que funcione debe utilizar diferentes servicios como el DNS, Kerberos o PKI.
# DNS
Un sistema de nombres de la organización distribuido y jerárquico.
Un servidor DNS se encarga de los nombre de su zona.
+ Dominio: Parte del espacio de nombres
+ Zona: Estructura en la que se almacena la información de gestión

Las direcciones se pueden ser resultas de manera directa o indirecta:

Los servidores DNS almacenan registros con información sobre el dominio y otros recursos, son los responsables de la resolución del dominio.
+ Servidor Primario: Contiene la copia original del fichero de zona, es donde se realizan las modificaciones, actualiza a los servidores secundarios mediante transferencias de zona.

+ Servidor Secundario: Contiene una copia del fichero de zona, es actualizado por el Primario y aporta balanceo de carga.

+ Servidor Caché: Únicamente almacenan resoluciones anteriores.

Los Forwarders son atajos usados para reducir el tiempo de resolución de un nombre, se suelen usar en nombres altamente recurrentes.

El DNS dinámico permite que los clientes se registren en el DNS y que los servidores puedan registrar los servicios que proporcionan todo de manera automática.

El DNSSEC está basado en una cadena de confianza, cada nodo puede autenticar al nodo jerárquicamente inferior.
Cada dominio envía a su superior su clave pública firmada por la clave privada.
# Kerberos
Es un servicio que permite el inicio de sesión único, usa tickets que prueban la identidad de un usuario en un servidor. Los usuarios solo necesitan iniciar. Este servicio usa un servidor de autenticación centralizado en el que todos confían (centro de distribución de claves).

El procedimiento es:
1. Envío de la solicitud pre-autenticación
2. Al comprobar la información se envía el TGT

Los servicios se pueden kerberizar para que solo usuarios con tickets accedan a estos.
1. El cliente envía un paquete TGS_REQ
2. El servidor comprueba si existe el SPN y que el TGT es correcto.
3. Tras esto el cliente envía el ticket de servicio
4. El servidor puede enviar un paquete para confirmar que es el servidor.

# LDAP
Base de datos de estructura jerárquica, permite centralizar toda la información de una organización, este organiza dicha información y la protege.

La información se distribuye por entradas, cada una tiene un atributo que un tipo y uno o más valores.

Un servidor LDAP sigue un esquema (Schema) que contiene clases de objeto y atributos. Las clases especifican el tipo de objeto que esta almacenado en la entrada, estos tienen atributos que pueden ser requeridos o permitidos.
Los objetos pueden ser de clases que heredan de otras clases. Todas las clases heredan de top.
![[Pasted image 20240424184135.png]]
![[Pasted image 20240424184415.png]]
El LDAP se compone de un modelo funcional que consta de de 3 categorías de operaciones: Autenticación, Interrogación (query) y Actualización.

Una query se lleva a cabo mediante los siguientes parámetros: Base, Ámbito, Filtro.

La actualización modifican el contenido del directorio

La autenticación tiene 3 niveles: anónimo, sin autenticación y autenticado.

El concepto de replicación permite tener varias copias del directorio distribuidas lo que provoca una mayor tolerancia a fallos y un aumento de eficiencia.

A la hora de llevar a cabo el diseño se debe tener en cuenta los siguientes aspectos.
+ Detectar la necesidad del directorio.
+ Identificar las fuentes de datos.
+ Crear el Schema.
+ Crear el esquema de nombres.
+ Determinar la ubicación de los servidores.
+ Determinar como se dividen los datos.
+ Seguridad.
# PKI
Autoridad certificadora, permite comunicaciones cifradas, controla certificados
# SSSD
Permite almacenamiento en caché, Demonio en los clientes FreeIPA
# NFS
Permite compartir información por a red, accediendo a info remota desde accesos locales, mejorando las prestaciones de seguridad y escalabilidad.

Para montarlo se debe editar el fichero /etc/exports de la siguiente manera
*directorio_a_compartir     ip_cliente1(permisos) ip_cliente2 (permisos)*

Por parte del cliente, este tiene que montar el recurso compartido, teniendo dos opciones:
mount: 
	*\#mount -t nfs4 nombre.servidor:recurso/compartido /ruta/destino*

editando el fichero /etc/fstab
	*nombre.servidor:/recurso/compartirdo /ruta/destino nfs (opciones) 0*

Este tipo de montaje estático presenta errores pues ralentiza el arranque y consume recursos. Para solucionar esto se recurre al automontaje evitando los problemas anteriores.
Su funcionamiento se basa en colocar puntos de escucha, al ser estos atravesados se invoca el automount. Estos puntos de escucha se declaran en /etc/auto.master:
*punto/escucha  fichero_mapa  opciones*

Los ficheros mapa deben tener la siguiente forma: /etc/auto.nombre

Estos deben tener la siguiente forma:
*clave opciones nombre.servidor:/ruta/absoluta*

siendo la clave el siguiente directorio tras el punto de escucha.
EJEMPLO DE MONTAJE DE HOME:
* \* nfs_server:/export/datos/&