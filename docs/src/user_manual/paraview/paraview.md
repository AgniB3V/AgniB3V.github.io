# Paraview

En este manual se describirán los pasos básicos a seguir para poder visualizar los resultados de la simulación en el software Paraview, se recomienda al usuario utilizar documentación externa en caso de querer hacer uso de funcionalidades mas complejas.

Comenzando en la pantalla principal de Paraview

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/c2af70ad-b82b-4e3b-837f-7a93a3c13e10"></center>
<center><i></i></center>

## Importación de resultados

Haciendo click en File -> Open

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/42fe20dc-f470-472b-b029-54a6c906166e"></center>
<center><i></i></center>

O bien click derecho dentro del recuadro Pipeline Browser

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/58c7383c-3994-4dde-89b8-6a3bffa64763"></center>
<center><i></i></center>

Se abrirá una ventana en la cuál podrán buscar los archivos de resultados, una vez en la carpeta donde estos se encuentran, se debera seleccionar el archivo .vtk.series

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/b9213e4e-99cc-44a3-b58b-6bf3e5fd7b10"></center>
<center><i></i></center>

Esto añadira al Pipeline Browser el archivo con los resultados

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/ddefabb3-94c2-4e01-9742-834f0353a91c"></center>
<center><i></i></center>

Para que estos sean visibles se debe hacer click en el boton con forma de ojo a la izquierda del nombre

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/41e76fce-4653-42f0-8ef4-170732517f26"></center>
<center><i></i></center>

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/9f9136d0-b6c4-419b-baef-045c558c8539"></center>
<center><i></i></center>

Una vez hecho esto se podrán visualizar los resultados

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/89abf75f-ef8f-4ba6-9de9-e5f23307d5eb"></center>
<center><i></i></center>

## Visualización a lo largo del tiempo

Para poder visualizar las temperaturas a lo largo del tiempo se debe ir View y activar Time Manager

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/6dcc0aae-ec75-45cd-9164-c95b160a7bfc"></center>
<center><i></i></center>

Esto abrirá el siguiente panel

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/65b4005f-d8ef-4b03-be51-998e1c733177"></center>
<center><i></i></center>

En este se podrá elegir que instante de tiempo se quiere visualizar

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/606266b1-d865-4566-bbdf-8fba96e8570f"></center>
<center><i></i></center>

Cabe aclarar que el rango de temperaturas a visualizar se mantiene constante cuando se cambia de instante, por lo que en casos en que los cambios de temperatura sean muy grandes, no se percibirán correctamente los resultados, para solventar esto, una vez seleccionado el instante que se quiere visualizar se debe hacer click en el siguiente boton para ajustar el rango de temperatura, el cual setea el minimo y el maximo correspondientes a las temperaturas de este instante

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/924a0cce-716e-44d8-935e-55b21e5c9f69"></center>
<center><i></i></center>

Se puede observar a continuación un ejemplo de como cambia el rango de temperaturas luego de clickear este boton

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/cbbbbef5-e0bb-4abe-a5cb-95ec9735b328"></center>
<center><i></i></center>

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/d43b3e1f-12d2-4288-9d82-7887977478a4"></center>
<center><i></i></center>

## Herramiente de Querys

Se recomienda el uso del siguiente panel para realizar consultas especificas sobre los datos.
Se debe ir a View y activar Find Data

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/0a1ceacc-3ce9-4047-ac35-27276aa889bf"></center>
<center><i></i></center>

El cual abre el siguiente panel

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/ad997ca9-a42c-48f9-ae89-8e9d170e84b9"></center>
<center><i></i></center>

Se debe seleccionar en Data Producer el vtk.series

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/2eb90d9c-b5fa-439f-a3fb-bdef24cf863a"></center>
<center><i></i></center>

En la primera parte se pueden seleccionar los criterios de busqueda, como si se va a buscar sobre puntos o celdas.

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/39c59a30-0ff1-4c4d-b5df-1442d9d17b72"></center>
<center><i></i></center>

En caso de buscar sobre puntos, se puede realizar la consulta sobre ID, Temperatura o Point (posicion x,y,z)

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/7f6f974a-af2f-4451-a90f-91001479e2a8"></center>
<center><i></i></center>

Luego se puede elegir la condición de busqueda y ingresar el valor

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/d0f210dd-2246-4288-bf76-b1123cf9dca3"></center>
<center><i></i></center>

Al clickear Find Data se realiza la busqueda

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/986f72ea-4326-4983-975d-b9df3fba620a"></center>
<center><i></i></center>

Esto generará puntos rosas sobre el modelo que indican que nodos cumplen con la condicion dada

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/6033e614-4bd1-4783-865a-00e7ea80b78f"></center>
<center><i></i></center>

Si se activa la siguiente opción, se podrá visualizar sobre cada nodo su ID o Temperatura

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/39829a3e-0c9e-4d83-a717-2d331e684d53"></center>
<center><i></i></center>

<center><img src="https://github.com/ThermalB3V/ThermalB3V.github.io/assets/39842759/be95f900-184f-4af6-9014-a6c3f66d66ad"></center>
<center><i></i></center>

Se debe tener en cuenta que si la consulta genera muchos resultados no todos los nodos mostrarán su ID, por lo que en caso de querer saber el ID de un nodo especifico se debe hacer una consulta que devuelva poca cantidad de nodos.