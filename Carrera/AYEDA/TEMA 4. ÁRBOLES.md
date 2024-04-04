#### Introducción.
Un árbol es un tipo de grafo en donde cada nodo es apuntado sólo por un nodo (menos el nodo raiz) y este puede apuntar a varios.

El grado del árbol determina el máximo de enlaces que puede tener un nodo. El árbol se organiza en niveles comenzando desde la raiz en 0, el número de niveles determina la altura del árbol.

Todo árbol se puede definir de manera recursiva, esto es, dentro de todo árbol se puede diferenciar otro y un árbol no pude compartir nodos con otro, los árboles que derivan del nodo raíz se determinan ramas.

Un camino es una secuencia de enlaces usados para llegar de un nodo a otro, el número de estos enlaces determinan la longitud.
#### Nodos.
Los nodos se pueden relacionar mediante enlaces como padre-hijo, abuelo-nieto o de hermanos. Estos últimos son aquellos nodos que estén en el mismo nivel.

Los nodos hoja no tienen hijos y los nodos interiores son aquellos nodos intermedios.
## Árbol binario.
Se define como un árbol que tiene grado máximo 2. De la raiz parten el sub-árbol izquierdo y el sub-árbol derecho. 
* El número máximo de nodos en el nivel n es 2^n.
* El número de nodos máximos en un árbol con profundidad p es 2^p - 1.
* El número máximo de hojas es 2^(profundidad - 1)

Un árbol se dice que está lleno cuando todos menos el último nivel están llenos.

Está equilibrado si la diferencia entre los dos sub-árboles es uno a lo sumo. Es perfectamente equilibrado si todas sus ramas están equilibradas

#### Ordenaciones.
Siempre se recorre de izquierda a derecha, los siguientes métodos definen en qué orden se registra la raiz de cada sub-árbol
###### Preorden.
Recorre la raiz antes que los dos sub-árboles.
RAÍZ ~ S IZQ ~ S DER
###### Postorden.
Recorre la raiz después de haber recorrido los sub-árboles.
S IZQ ~ S DER ~ RAÍZ
###### Inorden.
La raiz se recorre después de recorrer el primer sub-árbol.
S IZQ ~ RAÍZ ~ S DER
###### Por niveles.
Se registran los nodos de izquierda a derecha ordenados por nivel.
Se puede implementar con una cola en la que van entrando los hijos del nodo cabecera. En los casos de NULL se puede imprimir un carácter que indique que no tiene nada para que a la hora de representarlo sea más fácil ver el árbol.

###### \# Ejercicios
Al dar una secuencia de números se debe darse una secuencia en inorden y una secunda en post o pre orden. En base a la segunda secuencia se detecta la raiz, sabiendo esto se puede ver las dos ramas en el inorden y con esto solo queda operar de igual manera en el resto

#### Inserciones.
Se inserta como hijo de un nodo hoja. Hay que modificar los enlaces del árbol en el caso de que se quiera insertar en cualquier parte del árbol, aunque lo recomendables es insertar siempre abajo.

#### Eliminaciones.
De la misma forma que en la inserción hay que tener en cuenta si es un nodo hoja o interior a la hora de gestionar los enlaces.

Para eliminar un nodo se debe buscar con cualquier recorrido válido. Después hay que sustituir el valor del nodo a eliminar por el valor de un nodo hoja cuya eliminación no suponga un efecto en el equilibrio en el árbol (buscando en la rama con más nodos). Hay que tener en cuenta el tipo de árbol para ello: si en una rama hay positivos y en la otra negativos no se podría escoger la rama homóloga para encontrar el nodo
#### Implementación.
Cada nodo contiene 3 datos: el dato principal, y dos enlaces a sus hijos. El árbol tendrá un puntero al nodo raiz. 
###### Operaciones:
INICIALES:
+ Constructor
+ Destructor
+ Está vacío
+ Tamaño del árbol
+ Tamaño de la rama (Recursivo -> privado)
+ Altura del árbol
+ Altura de la rama (Recursivo -> privado)
+ Equilibrado (perfecto)
+ Equilibrado Rama (Recursivo -> privado)
RECORRIDOS:
INSERCIÓN:
ELIMINACIÓN:
