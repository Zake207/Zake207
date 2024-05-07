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
Se crean 3 sites: Planta alta (CD1, DNS), plantas medias(CD1 y CD2, DNS), planta baja.

# Ejemplo: Bob Esponja.
### Diseño lógico
Se creará un bosque, este poseerá dos dominios: "cc.com" y "cdc.com". A ser los nombres diferentes se crearan dos árboles.

Las unidades de control creadas dependen de las GPO's y la delegación de control. Para la delegación de control se obliga a crear OU's.

Al requerir una delegación de control en cc.com se deberá crear una OU para cocineros en dicho dominio. para el recurso compartido Cangreburger se pueden usar grupos locales y globales.
Para los robots si sería necesario crear una OU en cdc.com, a esta se le aplicará una GPO.

`site -> dominio -> OU

Para el fondo de pantalla se le puede aplicar una GPO de site, dentro del site se crea una OU para los jefes (OU de jefes en cc.com). Sin embargo no se puede solucionar el conflicto entre GPO pues se le asignan a ordenadores y usuarios.
Se puede, sabiendo los ordenadores de los jefes, añadirlos las OU de los jefes y hacer un filtrado de GPO's para que no les afecte.

Para que los jefes pueden acceder a las unidades montadas se debe usar la OU de jefes para poder montarles la unidad S: con DFS

NO VALE CON ILUSTRAR LAS OU, HAY QUE MOVER A LOS USUARIOS Y ORDENADORES. TRAS ESTO, EN EL DISEÑO HAY QUE AÑADIR LAS GPO'S Y DELEGACIONES DE CONTROL CADA OU. SIN OLVIDARSE DE LAS GPO'S APLICADAS A LOS SITES.

Faltan los permisos
Se le puede denegar el acceso a plankton

DFS.

Cuenta del servidor en dominio cc? se da por hecho
Forzar? no porque el forzado no afectaría a las máquinas.
Ejercicio?
### Diseño físico
SITES por cada uno un dns
controladores de dominio
