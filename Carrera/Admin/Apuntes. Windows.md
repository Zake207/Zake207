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
