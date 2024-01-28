# Interacción Elemento-Elemento

Para llevar cuenta de los factores de vista elemento a elemento se inicializa una matriz cuadrada con la misma cantidad de filas y columnas que de elementos. Los factores de vista no son simétricos, por lo que no se puede ahorrar cómputo o espacio en memoria con matrices triangulares.

Se emite la misma cantidad de rayos desde cada elemento y para cada rayo que colisionó se genera un número pseudoaleatorio entre cero y uno y se lo compara con la absortividad al espectro infrarrojo del material del elemento impactado. Si es menor, se suma uno a la fila del elemento emisor y la columna del elemento impactado. De lo contrario, se reemite el rayo desde la posición de la colisión en la dirección reflejada respecto a la normal del elemento. Tras considerar todos los rayos de un elemento, se divide la fila correspondiente por el total de rayos emitidos. Se introdujo un límite de reflexiones consideradas para asegurar que el algoritmo finalice en tiempo finito, aunque gracias a esto es posible que una fracción de rayos se pierdan cuando en la realidad no sería así.

Notar que los factores de vista elemento a elemento solo dependen de la geometría del modelo del satélite y, por tanto, alcanza con calcularlos una única vez.
