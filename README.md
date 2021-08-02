# TP3-Nosferatu

GRUPO UML || Algoritmos y Programacion 2 - 1C 2021 - Catedra: Juarez

INTEGRANTES:
- Gabriel Carniglia
- Sebastian Makkos
- Daniela Palacios
- Lara Galván

INTRODUCCION:
Luego de años de pelea llego el momento de la batalla final, los zombis y vampiros se han
aliado y buscan tener el control de todo el mundo. ¿Podrán los cazadores hacerles frente?
Para poder tener noticias de la batalla de forma segura se les pedirá a los alumnos de
algoritmos y programación II que creen un programa de generación de batallas para poder ver
los posibles resultados de la misma.

-------------------------------------- DISEÑO ----------------------------------------------

. MENU:
El juego cuenta con tres tipos de menu:
. Menu Inicial: Se muestran por pantalla las opciones de jugar, mostrar los créditos y salida
. Menu Juego: Aparecen las opciones para dar de alta o de baja un personaje, mostrar el tablero, buscar por
cuadrante un personaje u objeto, buscar por ID, iniciar simulacion y salida.
. Menu Simulacion: Se muestran las opciones para buscar por ID los detalles de un personaje u objeto,
mostrar el tablero, mostrar la cantidad de personajes de un bando, la seleccion del bando de cada jugador y
la salida.

. EJECUCION:
- Siempre que se termine una partida, o bien porque se guarda o bien porque se termino la simulación,
  se vuelve al menu principal (el de 3 opciones). Hay un bug que sucede cuando, al guardar la 
  partida cuando se ejecuta una nueva partida, se va al menu de las 7 opciones.

. JUGADORES:
- Hay 2 jugadores y cada uno tiene un bando (humanos o monstruos). Se elige aleatoriamente quien inicia el
  juego. Cada jugador interactua con los personajes pertenecientes a su bando con el objetivo de eliminar a los
  personajes del bando contrario. Si esto ultimo se logra, el jugador gana el juego.

. MOVIMIENTO:
- Los personajes no pueden pasar por encima de otros personajes. Al querer moverse por una
  posicion ocupada o a un casillero destino donde hay otro personaje se le informa al usuario la imposibilidad del
  movimiento.

- Al pasar por encima de un item, los personajes (dependiendo de cual sea el actual) los pueden agarrar.
  Los vampiros al pasar por encima de las estacas las destruyen.
  Los humanos solo pueden agarrar 1 sola escopeta, si pasan encima de otra, la ignoran.
  Los zombies pueden agarrar solamente agua bendita y pasan por arriba del resto de los items.

- Los personajes al estar encerrados por otros personajes no tienen la posibilidad de moverse a otra posicion, 
  se le informa al usuario con un mensaje de error de imposibilidad de llegada.
  

. ATAQUE:
Para atacar los personajes necesitan un minimo de energia. De no tenerlo, no pueden atacar.
- BANDO HUMANOS:
  Si los humanos quieren atacar a un zombie que esta en defensa bajo tierra o si quieren atacar 
  a Vampirella estando en modo murcielago, perderan su turno.
  Si los humanos no poseen armas en su respectivo Inventario, no pueden atacar.
  Si el personaje actual es Cazador o Vanesa, se le pregunta al jugador que arma desea utilizar. 
  El humano simple puede atacar solamente si posee una escopeta con un minimo de 2 balas.
  
- BANDO MONSTRUOS:
Los zombies muerden aleatoriamente a un humano cercano y lo transforma en zombie en 2 turnos
Los vampiros simples al atacar a los humanos que tengan menos de 30 puntos de vida los convierten 
  en vampiros.
Vampirella al atacar a los humanos les saca un punto de armadura permanentemente.
Nosferatu convierte a los humanos en vampiros. La conversion ocurre cuando termina de jugar el bando de los monstruos.
  
ACLARACIONES ATAQUE: 
- Cuando se ataca y se le quita puntos de cualquier tipo a un personaje se le aclara al usuario
  el daño general del mismo. Si un personaje tiene menos puntos de la cantidad de daño, se le decrementara hasta llegar 
  a cero.
  
- Cuando un zombie muerde a un personaje del bando Humanos esa conversión se realizara pasados 2 turnos


. DEFENSA:
Las defensas de los personajes requieren de un minimo de energia.
- BANDO HUMANOS:
Vanesa si cuenta con agua bendita en su inventario puede evitar que cualquier humano en un rango especifico se
convierta en zombie. Si cuenta con una cruz es inmune a cualquier ataque vampirico. Si no tiene ninguno
de estos dos elementos, se curara 10 puntos de vida
En la defensa de los cazadores se le pregunta al jugador si desea curarse a si mismo 50 puntos de vida o
curar a sus aliados 20 puntos de vida.
Los humanos simples si cuentan con agua bendita en el inventario pueden regenerar su energia o no usarla y ganar un 
punto de armadura por un turno. De lo contrario, ganan 3 puntos de energia.

- BANDO MONSTRUOS:
Los vampiros simples al defenderse se ocultan en las sombras ganando un punto de energia por un turno.
Nosferatu puede intercambiar su vida con la de un vampiro simple cercano, solo si es mayor a la suya.
Vampirella al defenderse se vuelve murcielago y no puede ser atacada por estacas ni agua bendita
por un turno.
  
ACLARACION TURNOS:
En cada ataque/defensa de algun personaje en la que se aclara que sus efectos son por uno o varios turnos,
esos efectos van a poder concretarse en la jugada inmediata despues. Por ejemplo, si Vampirella activa su 
defensa y le toca al bando de los humanos, esa defensa activada va estar haciendo efecto. Pero en la proxima
jugada de Vampirella esa defensa desaparece

. GRAFO:
El grafo usa Dijkstra con una cola de prioridad. Se utilizan 3 matrices, una llamada visitados que es de tipo bool, una
llamada costos de valores enteros y otra de recorridos, donde cada elemento es de tipo Coordenada. 
Esta ultima tiene una fila y una columna que corresponde al predecesor. Ademas se tiene una cantidad de iteraciones
desde casillero al recorrido. 
Se tiene el costo del casillero inicial hasta todos los posibles. Se extrae el valor requerido para el lugar donde se 
quiera llegar. Haciendo las validaciones previas correspondientes. 
Si no se puede llegar a una casilla que este ocupada o el personaje con el que se este jugando esta encerrado por otros,
aparece ese valor INFINITO (9999999) en la matriz.

. DICCIONARIO:
Para la creacion del diccionario se utilizo un Árbol Binario de Búsqueda. Cada Nodo del arbol tiene una clave asociada
de tipo entera, un puntero a Objeto, uno al Nodo izquierdo y derecho y un puntero al Nodo padre. 
El mismo tiene como objetivo realizar la busqueda por ID de los personajes para el juego.

. USO DE GOTOXY:
Aclaracion: La muestra del tablero se puede ver distorsionada si se agrandan las dimensiones del mismo.
