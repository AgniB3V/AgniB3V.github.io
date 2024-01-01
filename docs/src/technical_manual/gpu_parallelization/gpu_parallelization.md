# Paralelización en GPU

Para la paralelización en GPU se utilizó OpenCL. Específicamente la librería ocl de Rust.

OpenCL permite, entre otras cosas, ejecutar programas en GPUs, aprovechando asi la capacidad de paralelización de las mismas.

Aunque las GPUs permiten paralelizar muchas operaciones, cada una de estas es en si misma más lenta que la misma operación ejecutada en una CPU, por lo tanto, para obtener un speedup es necesario que la cantidad de operaciones a realizar sea grande, de forma tal que la paralelización de las mismas en GPU sea más rapida que su ejecución secuencial en CPU.

Es importante también aclarar que el pasaje de datos entre memoria de CPU y memoria de GPU es sumamente lento y debe limitarse lo máximo posible.

## Implementación

La forma de implementación fue la siguiente:

Se reemplazo la factorización LU por el calculo de la inversa de la matriz A, ya que la naturaleza propia de la resolución de los sistemas de ecuaciones lineales dadas las matrices L y U es de carácter secuencial, por lo que no era apta para su paralelización.

En cada iteración se calcula cuanto tiempo se puede correr la simulación hasta la proxima bajada de resultados y se manda a correr cada step a la GPU, una vez terminados, se obtienen los resultados del step actual. Esto permite que la comunicación entre CPU y GPU sea la minima posible.

Las distintas funciones que fueron pasadas a GPU son:

### Elevación a la cuarta

```
__kernel void fourth_elevation(__global double *t, __global double *t_4,
                               int n) {
  int i = get_global_id(0);
  if (i < n) {
    double t_i = t[i];
    double t_i2 = t_i * t_i;
    t_4[i] = t_i2 * t_i2;
  }
}
```

Esta función recibe un vector t de tamaño n y guarda en t_4 un vector donde cada elemento es el elemento de t elevado a la cuarta.
Cada hilo de ejecución calcula la elevación a la cuarta de un elemento del vector t, permitiendo asi la paralelización de esta operación.

### Multiplicación de matriz por vector (gemv)

```
__kernel void gemv1(__global const double *a, __global const double *x,
                    __global double *y, int m, int n) {
  double sum = 0.0f;
  int i = get_global_id(0); // row index
  for (int k = 0; k < n; k++) {
    sum += a[i + m * k] * x[k];
  }
  y[i] = sum;
}
```

Esta función recibe una matriz a de tamaño m x n, y un vector x de tamaño n y realiza la multiplicación de a * x, guardandolo en el vector y.
Cada hilo de ejecución realiza el calculo de una fila de la matriz a por el vector x.

### Suma de vectores

```
__kernel void vec_sum(__global double *a, __global double *b,
                      __global double *c, int n) {
  int i = get_global_id(0);
  if (i < n) {
    c[i] = a[i] + b[i];
  }
}
```

Esta función recibe un vector a y un vector b de tamaño n, y realiza la suma de ambos guardandolo en el vector c.
Cada hilo de ejecución realiza la suma de un elemento del vector a y b.

----------------------------------------------------

El proceso especifico realizado a partir de las funciones anteriores para resolver el sistema de ecuaciones es el siguiente:

Primero se utiliza la elevación a la cuarta para elevar el vector de temperaturas.

\\(t_4 = t ^ 4\\)

Luego se utiliza gemv para multiplicar la matriz H por la temperatura a la cuarta, guardandolo en el vector f.

\\(f = H * t_4\\)

Luego se utiliza la suma de vectores para actualizar el valor de f con los valores de f_const.

\\(f = f + f_{const}\\)

Se utiliza también gemv para la multiplicación de la matriz D por el vector de temperaturas, almacenandolo en el vector b.

\\(b = D * t\\)

Luego se utiliza la suma de vectores para actualizar el valor de b con la suma de b y f.

\\(b = b + f\\)

Por ultimo, se utiliza gemv para la multiplicación de la inversa de la matriz A por el vector b, obteniendo asi el nuevo vector de temperaturas.

\\(t = A^{-1} * b\\)