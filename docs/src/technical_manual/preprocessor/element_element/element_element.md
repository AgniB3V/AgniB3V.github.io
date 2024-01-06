# Interacción Elemento-Elemento

En línea con la descomposición en interacciones elemento-elemento descrita al comienzo de esta sección, debe calcularse para cada par de elementos la energía que intercambian. Como se emiten rayos en igual medida en todas direcciones, esto proporcional al factor de vista.

<center><img src="../images/view_factor.png" ...></center>

El factor de vista es la fracción del campo de visión que ocupa una superficie respecto a otra y el método más popular para su cómputo es Monte Carlo, en donde se seleccionan puntos del elemento emisor y direcciones al azar en la que se emiten rayos, se toma registro de los elementos impactados y luego se estima el factor de vista como la razón entre los rayos impactados y el total de rayos emitidos.

Introducir reflexiones es simple, para cada rayo que colisionó se genera un número pseudoaleatorio y se lo compara con el alphaSun del material del elemento impactado, si es menor se considera el rayo para el view factor del elemento impactado, de lo contrario se reemite el rayo desde la posición de la colisión en la dirección reflejada respecto a la normal del elemento. Se introdujo un límite de reflexiones consideradas para asegurar que el algoritmo finalice en tiempo finito, aunque gracias a esto es posible que una fracción de rayos se pierdan cuando en la realidad no sería así.

Notar que los factores de vista elemento a elemento solo dependen de la geometría del modelo del satélite, y por tanto solo deberán calcularse una única vez.
