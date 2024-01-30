# Resolución de sistemas de ecuaciones

Existen distintas técnicas para resolver sistemas de ecuaciones lineales. La más sencilla de todas implica hacer uso de la inversa de la matriz de coeficientes.

Dado el sistema de ecuaciones lineales

\\[
[A] \ \{x\} = \{b\}
\\]

Se obtiene el vector incógnita multiplicando el vector de términos constantes por la inversa de la matriz de coeficientes

\\[
\{x\} = [A^{-1}] \ \{b\}
\\]

Esta técnica tiene un punto positivo y uno negativo. Como punto positivo, una vez obtenida la inversa, esta puede ser utilizada tantas veces como sea necesario para iterar sobre la simulación y obtener las temperaturas de los nodos en cada paso de tiempo con una simple multiplicación. Como punto negativo, el algoritmo para computar la inversa requiere realizar un aproximado de \\(2n^3\\) operaciones para una matriz de \\(n \times n\\).

Una alternativa a este método es hacer uso de una descomposición LU, en la cual la matriz de coeficientes es descompuesta en dos matrices auxiliares L y U.

Dado el sistema de ecuaciones lineales
\\[
[A] \ \{x\} = \{b\}
\\]

Se realiza una descomposición de la matriz de coeficientes en una matriz L triangular inferior, y una matriz U triangular superior.

\\[
[A] = [L] \ [U]
\\]

Reemplazando en el sistema de ecuaciones

\\[
[L] \ [U] \{x\}= \{b\}
\\]

Que puede ser reescrito de la siguiente forma

\\[
\begin{aligned}
&[L] \ \{y\} = \{b\}\\\\[6pt]
&[U] \ \{x\} = \{y\}\\\\
\end{aligned}
\\]

Por ende, resolviendo secuencialmente ambos sistemas de ecuaciones, se podrá obtener la solución al sistema original. Ahora bien, gracias a que las matrices L y U son triangular inferior y superior respectivamente, es posible resolver ambos sistemas de ecuaciones en aproximadamente \\(2n^2\\) operaciones.

Por otro lado, el coste computacional de realizar la descomposición LU es de aproximadamente \\(\frac{2}{3}n^3\\) operaciones.

De esta forma, el costo computacional total para resolver el sistema de ecuaciones para una matriz de \\(n \times n\\) será:

\\[
\sim \frac{2}{3}n^3 + 2n^2
\\]

Esta técnica, al igual que la anterior, tiene un punto positivo y otro negativo. Como punto positivo, obtener la factorización LU es unas 3 veces más rápido que obtener la inversa de la matriz de coeficientes. Como punto negativo, cada vez que se requiera despejar un nuevo vector incógnita será necesario resolver los dos sistemas de ecuaciones de las matrices L y U antes detallado.

Otros algoritmos de resolución por métodos iterativos, como son el método de Jacobi, Gauss-Seidel y SOR también han sido estudiados. Sin embargo, todos ellos fueron descartados rápidamente, ya que requieren que la matriz de coeficientes sea diagonalmente dominante, característica que no puede ser asegurada para el dominio de este trabajo.


## Resolución en CPU

La ejecución del solver puede dividirse en dos etapas. 
Por un lado, se tiene la construcción de los datos necesarios para iniciar la simulación, esto es, las matrices y vectores locales y globales antes mencionados. 
Por el otro lado se tiene la propia ejecución de la simulación, resolviendo la ecuación principal en cada iteración de la misma.

Con el objetivo de contrastar los métodos de inversión de matriz y descomposición LU para la resolución del sistema de ecuaciones, 
se realizó una prueba sencilla, haciendo uso de un cubo de aproximadamente 10000 elementos y 5000 nodos. 
Sobre este modelo se realizó una simulación que consistió en 6000 pasos o iteraciones, totalizando 30000 segundos de simulación.

Como resultado se obtuvo que, para la etapa de construcción el algoritmo de LU fue un 6\% más lento que el algoritmo de inversión, 
mientras que para la etapa de simulación el algoritmo de inversión demoró un 131\% más. 
Esto se traduce en un speedup de 49\% a favor del algoritmo de descomposición LU. 
Adicionalmente, se compararon los resultados obtenidos entre ambos métodos y se computó el error absoluto medio, obteniendo un error de 0.04\%. 
Esto demuestra que, al menos para el dominio del problema, ambos métodos poseen la misma estabilidad numérica.

En base a esto fue que se decidió hacer uso del método de descomposición para la implementación del solver sobre CPU.

## Resolución en GPU

Llegado este punto se tiene una implementación funcional del solver que permite realizar simulaciones haciendo uso de la CPU. 
A partir de ahora, se buscará desarrollar una implementación que aproveche la potencia de la GPU, con la finalidad de reducir significativamente los tiempos de ejecución.

En contraste con las CPUs, las GPUs cuentan con un gran número de núcleos de ejecución. 
Una GPU moderna puede superar fácilmente los 3.000 núcleos, en comparación con los 12 núcleos de una CPU del mismo año. 
Sin embargo, es importante tener en cuenta que los núcleos de las GPUs son individualmente más simples y lentos en comparación con los núcleos de las CPUs. 
Además, se debe considerar la latencia en la transferencia de datos entre la memoria principal (RAM) y la memoria del dispositivo (GPU). 
Estas consideraciones se pueden resumir en las siguientes heurísticas clave al buscar optimizar la programación para GPU:

- El programa debe poder ser descompuesto en porciones capaces de ser ejecutadas de forma paralela.
- Se debe evitar interrumpir la ejecución de la GPU con transferencias entre la memoria principal y la memoria del dispositivo.
- Se deben limitar lo máximo posible los accesos del programa a memoria del dispositivo.

Los programas destinados a GPUs suelen ser mayoritariamente codificados en lenguajes basados en C, con pequeñas variaciones que añaden funcionalidades específicas, 
como la obtención de identificadores de proceso o la sincronización entre procesos. Estos programas se componen principalmente de funciones conocidas como kernels. 
Para la programación en GPU, se ha optado por el estándar multiplataforma y de código abierto OpenCL, haciendo uso de la biblioteca ocl de Rust como binding.

Como se ha mencionado, el solver puede dividirse en dos etapas: la construcción de los datos necesarios para la simulación y la ejecución propiamente dicha de la simulación. 
Esto implica que existen dos oportunidades distintas para lograr un aumento en la velocidad, especialmente si estas etapas son llevadas a cabo en una GPU.

El algoritmo de descomposición LU utilizado en la implementación para CPU presenta un comportamiento secuencial en la fase de solución de las ecuaciones lineales sobre las matrices triangulares. 
Esta característica reduce cualquier potencial mejora obtenida mediante la paralelización de operaciones en la GPU. 
Por este motivo, se tomó la decisión de implementar la solución en GPU utilizando el método de inversión de matriz.

El desarrollo de este método se dividió en dos fases. 
La primera tuvo como objetivo la inversión de la matriz de coeficientes, mientras que la segunda se dedicó a implementar las operaciones necesarias para realizar la simulación en la GPU.

En cuanto a la inversión de la matriz, se exploraron varios algoritmos, siendo el algoritmo de Gauss-Jordan el más destacado debido a su simplicidad y capacidad de paralelización. 
Sin embargo, debido a errores de concurrencia en la implementación este algoritmo aún no se encuentra integrado en el software. 

Para la segunda etapa se implementaron kernels basados en las funciones de GeMM (General Matrix Multiply), provenientes de la conocida biblioteca de álgebra lineal BLAS.

Los kernels implementados fueron:

``` C
__kernel void fourth_elevation(
    __global double *t, 
    __global double *t_4, 
    int n
);

__kernel void gemv1(
    __global const double *a, 
    __global const double *x, 
    __global double *y, 
    int m, 
    int n
);

__kernel void vec_sum(
    __global double *a, 
    __global double *b, 
    __global double *c, 
    int n
)
```

El kernel `fourth_elevation` recibe un vector de tamaño \\(n\\) conteniendo las temperaturas de los nodos y escribe el resultado de elevar cada componente de éste en el vector `t_4` del mismo tamaño. 
Para su ejecución se divide el trabajo en \\(n\\) work items.

El kernel `gemv1` realiza la multiplicación de la matriz `a` de dimensionalidad \\(m \times n\\) por el vector `x`, escribiendo el resultado en el vector `y`. 
Aquí se hace uso de una versión simplificada del algoritmo GEMM antes mencionado. 
Para su ejecución se divide el trabajo en \\(m\\) work items, cada uno de las cuales realiza el cómputo de una fila de la matriz `a`.

El kernel `vec_sum` realiza una suma entre los dos vectores `a` y `b` de tamaño \\(n\\) y escribe el resultado en el vector `c`. 
Para su ejecución se divide el trabajo en \\(n\\) work items.

Al momento de ejecutar la simulación, las operaciones generadas son encoladas por parte de la CPU a una cola de trabajo que provee OpenCL como medio de comunicación con la GPU. 
Gracias a la forma en la cual las operaciones fueron construidas, 
es posible ejecutar varias iteraciones de la simulación sin necesidad de realizar transferencias de datos entre la memoria de la GPU y la memoria principal. 
Antes de comenzar la ejecución, el programa en CPU calcula el número de iteraciones a realizar y encola exactamente el número de operaciones acordes a este, 
tal que la GPU se mantenga ocupada de manera ininterrumpida. 
El número de iteraciones a realizar estará relacionado con la necesidad de obtención de resultados parciales por parte de la CPU, 
o a la actualización del vector de flujos constante, el cual tiene dependencias con la posición del satélite en la órbita.




