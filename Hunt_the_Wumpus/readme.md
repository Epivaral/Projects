 # HUNT THE WUMPUS - Eduardo Pivaral Leal

## Descripcion del proyecto 




  
 * Tablero de 20X20, donde el jugador se puede mover arriba, derecha, abajo, izquierda, 
   excepto en los bordes donde solo hay 3 movimientos posibles,
   o en las esquinas donde solo hay 2 movimientos posibles

   ![image](https://github.com/Epivaral/Projects/assets/39424641/1250c77a-11f9-41c5-8333-3742f5bce8b8)

 * El Agente puede ganar de 2 maneras:
   - Encontrando el oro
   - Matando al Wumpus
 
 * Informacion de los items (todos se colocan en posiciones aleatorias):
 * ![image](https://github.com/Epivaral/Projects/assets/39424641/0791be1e-36d9-43d9-b0b8-0623e2b159cb)
   
   - ORO (x1) : Al encontrarlo GANAS el juego. No hay notificacion de su ubicacion en ninguna habitacion contigua.

   - WUMPUS (x1) : Si lo encuentras te come y PIERDES el juego. al estar en una habitacion contigua recibes el mensaje "Sientes un olor terrible"
        - Al estar en una habitacion contigua puedes matarlo de un disparo, si aciertas GANAS el juego, si fallas tendras que regresar y seguir explorando por otro camino. 
        - Si ya no cuentas con disparos tendras que regresar y seguir explorando por otro camino.

   - Agujero (x4) : Si lo encuentras caes en el y PIERDES el juego. al estar en una habitacion contigua recibes el mensaje "Sientes una brisa"
        - Al estar en una habitacion contigua, regresas y sigues explorando por otro camino.
    
   - Murcielago (x8): Si lo encuentras, te atrapa y te teletransporta a una ubicacion aleatoria de la cueva.
        - Al estar en una habitacion contigua recibes el mensaje "Escuchas un aleteo"
        - En este caso, si es la primera vez que visitas la habitacion contigua, sigues adelante con la exploracion (con el peligro de ser teletransportado)
        - Para siguientes ocasiones, evitas esa habitacion si debes volver a visitarla.
        - Si un murcielago te teletransporta, todo tu historial de exploracion se borra y deberas explorar toda la cueva de nuevo, excepto por las amenazas previamente marcadas, estas si podras evitarlas en tu nueva exploracion.
  
 * El Agente no cuenta con ninguna informacion al principio del juego y empieza en una ubicacion aleatoria
    
 * La cueva se explora usando un algoritmo Depth First Search, y cuando estamos en una habitacion contigua a un peligro, regresamos al nodo padre de nuestro arbol de exploracion.
 
 * El Agente guarda la siguiente informacion, la cual se va llenando conforme avanza en la exploracion:
   - Nodos explorados
   - Stack de "nodo anterior" para el algoritmo DFS (para que sepa como regresar en el arbol de busqueda)
   - Nodos contiguos "peligrosos" (se evitan estas casillas en el futuro para minimizar el peligro)
 
 * En el caso en que nuestro arbol de exploracion este vacio (estamos en el nodo inicial), nos movemos hacia la siguiente casilla disponible, con el peligro de caer en un peligro y perder el juego.
  
 * El agente cuenta con 2 disparos para matar al Wumpus en caso de encontrarse en una habitacion contigua, el disparo se realiza hacia una habitacion aleatoria y puede acertarse o fallarse.
   que se hace en cada caso se discute en la seccion de Wumpus. 

 * Existe una probabilidad muy alta (mas del 90% segun 2,200+ juegos simulados) de ganar el juego, ya que el algoritmo DFS es un algoritmo completo, 
   y el agente unicamente pierde el juego en estos casos:
   - El nodo inicial esta contiguo a una amenaza y al no tener un historial de nodos peligrosos, debe continuar la exploracion y el agente puede encontrar el peligro.
   - Al ser teletransportado por un murcielago se borra el arbol de busqueda y se inicia la exploracion de nuevo (caso similar al de arriba).
   - Cuando la exploracion ya esta muy avanzada y el numero de nodos pendientes es muy pequeño, y el agente por fuerza deba arriesgarse a continuar la exploracion por un nodo posiblemente peligroso.


 * Al iniciar el juego se presentan unicamente al espectador, la ubicacion de las amenazas y el oro (fondo azul), esta informacion es ignorada por el Agente
 * Durante el juego se va presentando la casilla actual, proximas casillas y si hay algun peligro
 * Luego se muestra la decision que el agente tomo para cada casilla
 * Al finalizar el juego se muestran las estadisticas del juego. Luego tenemos la opcion de repetir el juego.

 ## Dependencias
    pip install <dependencia>

 * colorama
 * operator
