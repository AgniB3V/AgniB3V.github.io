Modelo teórico
==============

Transferencia de Calor
----------------------

El calor se transfiere de 3 maneras:

*   Convección
*   Conducción
*   Radiación

Dado que la densidad del aire a altitudes muy elevadas es extremadamente baja, desde la órbita terrestre baja (LEO) en adelante, el aire disponible para la refrigeración natural es insignificante, por lo que no hay convección. La transferencia de calor en el espacio está principalmente controlada por la conducción y la radiación.

Sin convección natural para enfriar la electrónica, un sistema que funciona con la misma potencia en el espacio es más probable que alcance una temperatura más alta en comparación con uno que opera a nivel del mar.

### Transferencia de Calor por Conducción

La transferencia de calor puede ocurrir dentro de un material o entre dos o más cuerpos en contacto. Está dada por la Ley de Fourier, en una dimensión:

\\(q^{''}_x = -k \frac{dT}{dx}\\)

*   q es la tasa de flujo de calor (\\(\frac{W}{m^2}\\))
*   k es la conductividad térmica (\\(\frac{W}{m *K}\\)) del material
*   \\(\frac{dT}{dx}\\) es la diferencia de temperatura a lo largo de la longitud

A diferencia del modo de transferencia de calor por convección, la resistencia a la conducción dentro del sólido no cambia con la altitud.

En el caso más general, la ecuación se expresa en forma diferencial

\\(c p \frac {\partial T}{\partial t} = k * (\frac {\partial^2 T}{\partial x^2} + \frac {\partial^2 T }{\partial y^2}  + \frac {\partial^2 T }{\partial z^2}) + q_v\\)

Siendo c el calor específico, p la densidad y \\(q_v\\) el calor generado

### Transferencia de Calor por Radiación

La transferencia de calor por radiación ocurre entre dos o más superficies a través de ondas electromagnéticas. Depende de la temperatura y del revestimiento de la superficie radiante.
Un cuerpo negro es el emisor más eficiente, la radiación que emite a una temperatura T (K) sigue la Ley de Stefan-Boltzmann:

\\( E = \sigma T^4 \\)

*   σ es la constante de Stefan-Boltzmann -> \\(5.63 * 10^{-8} \frac{W}{m^2 K^4}\\)
*   E es el calor emitido por unidad de area por un cuerpo negro \\([\frac{W}{m^2}]\\)

Si multiplicamos por el area radiante, obtenemos:

\\( E_r = A^r \sigma T^4 \\)

*  \\(E_r\\) es el calor absoluto emitido por un cuerpo negro [W]

Un cuerpo que no emite con la misma eficiencia que un cuerpo negro se conoce como cuerpo gris, la radiación emitida por un cuerpo gris es:

\\( E_{gris} = ε A^r \sigma T^4 \\)

*  Siendo ε la emisividad del cuerpo gris

La cantidad de energía transferida por radiación entre dos objetos con temperaturas \\(T_1\\) y \\(T_2\\) se encuentra con:

\\( q_r = ε \sigma F_{1,2} A (T_1^4 - T_2^4)\\)

*   \\(q_r\\) es la cantidad de transferencia de calor por radiación (W)
*   ε es la emisividad de la superficie radiante (reflectante = 0, absorbente = 1)
*   \\(F_{1,2}\\) es el factor de vista entre la superficie del cuerpo 1 y el cuerpo 2 (≤1)

El factor de vista entre dos superficies se define como la porción de la radiación saliente de una superficie que es interceptada por la otra.

A menos que la diferencia entre dos o más cuerpos sea alta, la transferencia de calor por radiación suele ser muy baja.

*   La radiación entre el sol y el satélite debe ser tenida en cuenta..
*   La radiación entre los componentes electrónicos internos puede ser desestimada.

Fuentes de Calor en Sistemas Espaciales
---------------------------------------

Hay generalmente tres fuentes de calor:

![](images/image3.png)

*   Radiación del sol
*   El albedo
*   Calentamiento planetario proveniente de la Tierra (radiación de cuerpo negro de la Tierra)

* * *

### Radiación solar

Es la principal fuente de calentamiento, puede ser considerada constante, suele rondar entre 1322 \\(\frac{W}{m^2}\\) y 1414 \\(\frac{W}{m^2}\\)

El cálculo de la radiación incidente desde el sol sobre una superficie se caracterizapor el flujo solar, S \\([\frac{W}{m^2}]\\) y por su orientación respecto al sol.
Debido a la gran distancia con el sol, se puede tomar la suposición de que la radiación esta esta dada por rayos paralelos.

Hay que tener en cuenta que las superficies poseen una absortividad en el espectro de luz solar, por lo que no necesariamente absorberan toda la radiación proveniente del sol.

### Albedo

El albedo es la radiación solar reflejada desde la superficie terrestre. Se suele expresar como la fracción de radiación solar incidente que es reflejada hacia el espacio.

\\( A = f S\\)

* A, flujo de Albedo \\([\frac{W}{m^2}]\\)
* f, factor de albedo
* S, constante solar \\([\frac{W}{m^2}]\\)

El albedo promedio de la tierra es de aproximadamente 0.3.

Se debe tener en cuenta que la orientación del satétile respecto a la tierra influirá sobre la radiación absorbida por albedo, asi como también influirá la absortividad en el espectro solar, al igual que en la radiación solar.

### Radiación Infraroja Terrestre

La radiación Infraroja (IR) terrestre refiere a la radiación emitida por la tierra por el simple hecho de tratarse de un cuerpo con temperatura mayor a cero grados absolutos. Por lo general se considera que esta radiación es constante a lo largo de su superficie y se la suele tomar con un valor cercano a 235 \\(\frac{W}{m^2}\\).

Al igual que con el Albedo, la orientación del satétile respecto a la tierra influirá en la radiación absorbida por este, también influirá la absortividad en el espectro IR (distinta a la solar) del material utilizado.

* * *
