# Modelo FEM

Para resolver el problema de transferencia de calor se utilizaron métodos numéricos, particularmente el modelo de elemento finitos (FEM).
Este método consiste en dividir el modelo en elementos de dos dimensiones, en nuestro caso triangulares, en los cuales los vertices de cada triangulo conforman nodos.

La ecuación que gobierna la transferencia de calor es la siguiente:

$c p \frac {\partial T}{\partial t} = \frac {\partial }{\partial x} (k_x\frac {\partial T}{\partial x}) + \frac {\partial }{\partial y} (k_y\frac {\partial T}{\partial y}) + q_v$

Siendo c la capacidad térmica, p la densidad, $k_x$ y $k_y$ las conductividades térmicas en cada dirección.

La condición inicial necesaria para resolver es 

$T(x,y,t)|_{t=0} = T_0(x,y)$

Para la resolución de estas ecuaciones se tomó una expresión matricial de las mismas, para mas información sobre el proceso matématico para llegar a estas ecuaciones referirse al siguiente paper [Finite Element Method in Steady-State and Transient Heat Conduction](https://www.researchgate.net/publication/274399522_Finite_Element_Method_in_Steady-State_and_Transient_Heat_Conduction)

$ [M^e] \{\frac {d T^e}{dt}\} + [K^e] \{ T^e \} = \{ f^e\}$

Siendo $ [M^e] $ la matriz de capacitancias , $[K^e]$ la matriz de conductividad y $\{ f^e\}$ el vector de flujos. Todas relativas a un elemento.

A esta ecuación se la conoce como la representación de Galerkin de la ecuación de transferencia de calor transitoria.

Se tomo la decision de que el vector $\{ f^e\}$ solo contenga flujos constantes, ya que esto facilita la integración del método con las fuentes de calor propias de un satélite en órbita.

Para poder generar estas matrices, se deben primero obtener matrices locales a nivel elemento, para luego a partir de estas generar las matrices globales.
El proceso de generación de las matrices globales es el siguiente:

Partimos de un ejemplo de un modelo con 2 elementos y 4 nodos, la numeración global es la siguiente:

![](images/image1.png)

Y la numeración local:

![](images/image2.png)

Para obtener las matrices globales, se toman los valores correspondientes en las matrices locales utilizando los ids de nodos globales, y estos se suman en la matriz global.

![](images/image3.png)
![](images/image4.png)

Una vez hecho esto se obtienen las matrices globales, formando asi la sigiuente ecuación:

$ [M] \{\frac {d T}{dt}\} + [K] \{ T \} = \{ f\}$

Se utilizó el metodo generalizado de Crank-Nicolson, obteniendo asi la siguiente ecuación:

$ (\frac{1}{\Delta t}[M] + \theta [K]) \{ T \}^{n+1} = [ \frac{1}{\Delta t}[M] - (1- \theta) [K] ] \{T\}^n + (1- \theta) \{f\}^n + \theta \{f\}^{n+1} $

En nuestro caso se utiliza $\theta = 0.5$ , llamado esquema semi-implicito, método de Cranck-Nicolson

Para obtener las matrices locales para cada elemento, dado un elemento generico

![](images/image5.png)

Definimos:

$b_1^e = y_2 - y_3$

$c_1^e = x_3 - x_2$

$b_2^e = y_3 - y_1$

$c_2^e = x_1 - x_3$

$b_3^e = y_1 - y_2$

$c_3^e = x_2 - x_1$
 
Luego la matriz de conductividad del elemento $[K_c^e]$, tiene la forma

$[K_c^e] = \begin{bmatrix}
K^e_{11} & K^e_{12} & K^e_{13}\\
K^e_{21} & K^e_{22} & K^e_{23}\\
K^e_{31} & K^e_{32} & K^e_{33}
\end{bmatrix} $

Se toma que $k_x = k_y = k$, es decir, los materiales poseen la misma conductividad en ambas direcciones

$A^e$ es el area del elemento

$K^e_{11} = \frac{k}{4A^e} ((b^e_1)^2 + (c^e_1)^2)$

$K^e_{12} = \frac{k}{4A^e} ((b^e_1 * b^e_2) + (c^e_1 * c^e_2))$

$K^e_{13} = \frac{k}{4A^e} ((b^e_1 * b^e_3) + (c^e_1 * c^e_3))$

$K^e_{21} = K^e_{12}$

$K^e_{22} = \frac{k}{4A^e} ((b^e_2)^2 + (c^e_2)^2)$

$K^e_{23} = \frac{k}{4A^e} ((b^e_2 * b^e_3) + (c^e_2 * c^e_3))$

$K^e_{31} = K^e_{13}$

$K^e_{32} = K^e_{23}$

$K^e_{33} = \frac{k}{4A^e} ((b^e_3)^2 + (c^e_3)^2)$

Luego la matriz de capacitancia del elemento $[M^e]$

$[M^e] = \frac{A^e}{12} c p \begin{bmatrix}
2 & 1 & 1\\
1 & 2 & 1\\
1 & 1 & 2
\end{bmatrix}$

Y el vector de flujos $\{f^e\}$

$\{f^e\} = q \frac{A^e}{3} \begin{bmatrix}
1 \\
1 \\
1 
\end{bmatrix}$

Siendo q el flujo sobre el elemento

Todo el desarrollo hasta el momento se planteo desde el punto de vista de un modelo 2D, sin embargo en nuestro caso nos encontramos ante modelos 3D, la decisión tomada dada la naturaleza del problema, en el cuál se suelen modelar los satélites como placas de grosor fijo fue la de adaptar este modelo a uno "2.5 D", en el cuál se realiza el mallado del elemento tridimensional en dos dimensiones a lo largo de su superficie, y cada elemento particular queda en dos dimensiones, pero con coordenadas en 3D.

Los cambios que esto añade al modelo son los siguientes:

Se incorpora el parametro relativo al grosor, modificando asi las siguientes ecuaciones:

Para todos los i,j pertenecientes a $K^e$:

$K^e_{ij} = grosor *  K^e_{ij}$ 

$[M^e] = \frac{A^e}{12} grosor *  c p \begin{bmatrix}
2 & 1 & 1\\
1 & 2 & 1\\
1 & 1 & 2
\end{bmatrix}$

Luego los calculos de los $b_i$ y $c_i$ que dependen de los puntos en el espacio del triangulo, puede observarse que en realidad son todos propiedades intrinsecas del mismo.

$(b^e_1)^2 + (c^e_1)^2$ es la distancia al cuadrado entre el vertice 2 y el vertice 3 del elemento.

Analogamente, $(b^e_2)^2 + (c^e_2)^2$ es la distancia al cuadrado entre el vertice 1 y el vertice 3 del elemento.

Y $(b^e_3)^2 + (c^e_3)^2$ es la distancia al cuadrado entre el vertice 1 y el vertice 2 del elemento.

Luego, 

$(b^e_1 * b^e_2) + (c^e_1 * c^e_2)$ se puede interpretar como el producto escalar entre dos vectores, el primero es el que une el vertice 2 y el 3, y el segundo el que une el vertice 3 y 1

Analogamente

$(b^e_1 * b^e_3) + (c^e_1 * c^e_3)$ se puede interpretar como el producto escalar entre dos vectores, el primero es el que une el vertice 2 y el 3, y el segundo el que une el vertice 1 y 2

$(b^e_2 * b^e_3) + (c^e_2 * c^e_3)$ se puede interpretar como el producto escalar entre dos vectores, el primero es el que une el vertice 3 y el 1, y el segundo el que une el vertice 1 y 2

Por lo tanto, todos estos calculos pueden realizarse a partir de las coordenadas de los vertices en 3D.
