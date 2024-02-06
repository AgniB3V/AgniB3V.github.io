# Plotter

## Ejecución

En caso de desear ejecutar el Plotter por fuera de la GUI, se debe ejecutar el siguiente comando:

``` bash
python3 UI.py
```

## Uso del Plotter

La interfaz de usuario del Plotter corresponde con lo que se muestra en la siguiente captura:

<center><img src="images/a.png" ...></center>

Para cargar los datos de la simulación será necesario presionar el botón "*Choose File*". Esto abrirá una nueva ventana en la cual se podrá seleccionar el archivo
`*.vtk.series` deseado.

<center><img src="images/b.png" ...></center>

El tiempo de carga de los resultados dependerá del tamaño del modelo y la cantidad de archivos generados.

<center><img src="images/c.png" ...></center>

Tras finalizar la carga se indicará el path del archivo procesado.

<center><img src="images/d.png" ...></center>

Existen 4 graficos distintos que se pueden seleccionar. El primero, "All Temperatures Over Time" muestra un grafico de la temperatura en relacion al tiempo con una linea para cada nodo.

<center><img src="images/e.png" ...></center>

El segundo, "Temperature Over Time" permite visualizar la temperatura de un solo nodo a elección, para lo cuál se debe indicar su ID. Referirse al manual de Paraview para obtener el ID de un nodo.

<center><img src="images/f.png" ...></center>

<center><img src="images/g.png" style="margin-top:10px" ...></center>

El tercero, "Average Temperature Over Time" muestra la temperatura promedio de los nodos a través del tiempo.

<center><img src="images/h.png" ...></center>

El cuarto, "Standard Deviation Over Time" muestra la desviación estándar de la temperatura de los nodos a través del tiempo.

<center><img src="images/i.png" ...></center>
