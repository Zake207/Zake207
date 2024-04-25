#### Perfiles.
+ Perfil por defecto: la base para el resto.
+ Perfil Local: Se crea la primera vez que el usuario entra en el ordenador.
+ Perfil Flotante: Se crea por el administrador y se almacena en un servidor, estando disponible desde cualquier ordenador de la red.
+ Perfil Obligatorio: Creado para especificar una configuración particular de los usuarios, pudiendo ser local o flotante.
#### Grupos.
Colección de cuentas de usuario y permiten simplificar el acceso a los recursos.
###### Tipos:
**Grupos de seguridad:** Usados para cualquier asunto relacionado con el tópico.
**Grupo de distribución:** Usados para el resto de asuntos.
###### Ámbitos:
Determinan dónde se puede utilizar dicho grupo.
+ Global del dominio: Son visibles para el resto de dominios del bosque pero sólo puede contener miembros y grupos anidados del mismo dominio que el grupo.
+ Local del dominio: Solo es visible en el dominio donde se define, pero puede contener usuarios y grupos globales anidados de cualquier otro dominio.
+ Universales: Se le pueden asignar miembros de cualquier dominio y se le puede asignar permisos en todos los dominios del árbol, no están asociados a ningún dominio sino que residen en el catálogo global.
###### Recomendaciones:
![[Captura desde 2024-04-02 17-31-48.png]]
+ No usar universales
+ Meter un usuario en un grupo global, al recurso darle permisos en un grupo local y luego metemos e grupo global en el grupo local.
#### Distribución de información
Distribuido
Centralizado

La info se guarda en diferentes formatos FAT, FAT32, extFAT, NFTS.

Se puede acceder a la información de manera local o de manera remota
### Control de accesos
###### **Permisos NTFS**
A nivel de sistema de archivos.
Almacena una lista de control de acceso, cuando a un recurso intenta entrar un usuario que no tiene entrada en esta lista se le deniega el permiso. El permiso denegar prevalece sobre el resto. Los permisos son acumulativos y en caso de que haya varias coincidencias los permisos son la suma.

Los permisos son heredados y propagados, se puede evitar esta herencia y primera carpeta después de esta herencia se convierte en padre de las descendientes de esta.
Hay dos opciones para eliminar la herencia: Copiar y borrar.


###### **Permisos compartidos**
Solo se aplican cuando se accede por la red. Utiliza una ruta universal para acceder a la carpeta compartida: \\\\desktop.elderring.com\\dinerito
El recurso compartido tiene un nombre que se le asigna para ser compartido, en este caso es *dinerito* 

Los permisos compartidos se establecen a nivel de carpeta y se aplica a todo su contenido, suele ser el menos restrictivo para que los NFTS controlen los permisos de mejor manera.

###### Permisos especiales
Son permisos individuales para los archivos. Es mejor no asignarlos. La idea es tratar de "no permitir" antes que "denegar".

#### Diseño Lógico.
+ Cada CD gestiona un único dominio. No se pueden borrar.
+ Tratar de tener un único dominio con varias Unidades Organizativas siempre que sea posible.
+ Saber la estructura de la organización. Establecer un criterio de nombres para la red.
+ Organizar la info interna y hacer las GPOs.

Al pedir diseñar una organización hay que responder las siguientes cuestiones:
###### nº de bosques 
Un bosque por lo general, hay excepciones: unidades de la organización independientes o razones políticas. La más común es por la necesidad de tener esquemas(clases o atributos) diferentes.
###### nº de dominios
Un solo dominio salvo que: 
+ Se quiera dividir las tareas de administración.
+ Diferentes duración de los tickets de kerberos
+ Diferentes desvíos en la hora del sistema.
+ Para optimizar el sistema o comunicaciones Teniendo diferentes CD(controladores de dominio) para minizar el tráfico de baja replicación.
El cómo organizarlos depende de los nombres otorgados a los dominios, siempre tratar de tener el menor número posible de dominios.
###### Unidades organizativas
Debe tener un diseño independiente en cada dominio.
Se crean para tener una mejor delegación de control y poder organizar las GPO's. Son anidables aunque no se recomienda pasar de los 3 niveles de anidación.
###### Grupos y permisos
Se resuelve en la estructura física.
#### Estructuras.
![[Pasted image 20240409175224.png]]

#### Diseño Físico
Implementa la estructura lógica de la organización en la estructura física de red, este optimiza el tráfico en las lineas de baja velocidad.

Este diseño permite crear grupos de directivas aunque no eliminan la replicación. También tiene el riesgo dar problemas de consistencia.
La replicación sigue el modelo multimaster, pero hay algunas operaciones críticas que no se pueden realizar.

Además hay cierta información que puede ser compartida por todos los controladores del árbol y otra que es compartida solo por los controladores del dominio

Entre los diferentes sites se establecen enlaces, estos tienen un coste, que no es más que la representación de la velocidad y fiabilidad atribuido a los enlaces usado para calcular los caminos entre sites
Se replican: Las modificaciones
Como se replican: Intrasite, Infrasite
###### Intersite
El admin establece los sites.
Por cada partición/base de datos establece un anillo
Para diferentes sites se programa la hora de replicación y se replica la información entre los cabezas de puente
###### Infrasite
Son inmediatas y automáticas

## Directivas de grupo
Los parametros pueden tener 3 valores: Habilitado, deshabilitado y no configurado.

## Aplicación de las GPO's
Están asociadas a sitios, dominios o unidades organizativas.
Permiten establecer directivas globales sobre esos contenedores.

# DFS
Consiste en crear una estructura de carpetas manejable y visible para los usuarios, la localización real de los archivos es invisible para los usuarios. Se instala añadiendo roles y características. Además los ficheros se pueden replicar si están enlazadas a la misma carpeta.
+ Basado en dominio: Acceso del tipo \\\\ull.es\\carpeta. No depende de un servidor
+ Basado en servidor: El acceso es contiene el nombre de la máquina en vez de el del dominio.
La replicación permite crear réplicas de los datos para mejorar los accesos, solo se guardan los cambios más recientes.
# Ejemplo: softlab

Un bosque con un dominio.
De este dominio se crea un site (plantabaja) a ese site se le añade la correspondiente GPO con la restricción dictada.

Se crean los grupos globales de desarrollo y dirección
GG_desarrollo
GG_dirección

Para poder imprimir en todas las impresoras de la empresa se debería crear un grupo local que al que se le dan los permisos

Luego hay dos carpetas ficticias para la cual se crean dos grupos locales, uno que de control total, y otro de leer.

Meto a los admins en el de impresora y lectura, a los desarrolladores solo se les mete en el de control total

Para montar la unidad H que solo se le monte a los desarrolladores se debe crear una OU sobre la que se le aplique la GPO de asignación de unidades. Si no se hiciera la OU, aunque no se le permita entrar, se le montaría igualmente al resto.

Hay que montar una DFS en el que se engloben las dos carpetas y montar la carpeta englobante en el dfs.

Por otro lado el diseño físico
Se crean 3 sites: Planta alta (CD1, DNS), plantas medias(CD1 y CD2, DNS), planta baja
