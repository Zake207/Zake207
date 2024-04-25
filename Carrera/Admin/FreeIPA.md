Gestiona los usuarios y máquinas de una entidad, también establece políticas para operar con los servicios e información.

Para que funcione debe utilizar diferentes servicios como el DNS, Kerberos o PKI.
# DNS
Un sistema de nombres de la organización distribuido y jerárquico.
Un servidor DNS se encarga de los nombre de su zona.
+ Dominio: Parte del espacio de nombres
+ Zona: Estructura en la que se almacena la información de gestión
Las direcciones se pueden ser resultas de manera directa o indirecta:
+ Directa:
+ Indirecta:

Los servidores DNS almacenan registros con información sobre el dominio y otros recursos, son los responsables de la resolución del dominio.
+ Servidor Primario: Contiene la copia original del fichero de zona, es donde se realizan las modificaciones, actualiza a los servidores secundarios mediante transferencias de zona.

+ Servidor Secundario: Contiene una copia del fichero de zona, es actualizado por el Primario y aporta balanceo de carga.

+ Servidor Caché: Únicamente almacenan resoluciones anteriores.

Los Forwarders son atajos usados para reducir el tiempo de resolución de un nombre, se suelen usar en nombres altamente recurrentes.

El DNS dinámico permite que los clientes se registren en el DNS y que los servidores puedan registras los servicios que proporcionan.

El DNSSEC está basado en una cadena de confianza, cada nodo puede autenticar al nodo jerárquicamente inferior.
Cada dominio envia a su superior su clave pública firmada por la clave privada.
# Kerberos
Permite un inicio de sesión único y trabaja en base a tickets
# LDAP
Base de datos de estructura jerárquica, permite centralizar toda la información de una organización, este organiza dicha información y la protege.

La información se distribuye por entradas, cada una tiene un atributo que un tipo y uno o más valores.

Un servidor LDAP sigue un esquema (Schema) que contiene clases de objeto y atributos. Las clases especifican el tipo de objeto que esta almacenado en la entrada, estos tienen atributos que pueden ser requeridos o permitidos.
Los objetos pueden ser de clases que heredan de otras clases.
![[Pasted image 20240424184135.png]]
![[Pasted image 20240424184415.png]]
El LDAP se compone de un modelo funcional que consta de de 3 categorías de operaciones: Autenticación, Interrogación (query) y Actualización.
# PKI
Autoridad certificadora
# SSSD
Permite almacenamiento en caché
