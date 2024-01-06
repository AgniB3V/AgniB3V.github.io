# Preprocesador

El modelo tridimensional del satélite, junto con los materiales asignados a cada polígono que lo compone, son información suficiente para el cálculo de la transmisión de calor por conducción y estos datos se encuentran estructurados de forma tal que es preciso y eficiente considerar solo el aporte de la vecindad para cualquier punto en un tiempo determinado.

Para la transmisión de calor por radiación deberán contemplarse además la posición de la Tierra y el Sol, así como el modo en que las distintas partes del satélite eclipsan a otras. La energía recibida en un punto es el resultado de integrar los rayos que fueron emitidos/reflejados por otros cuerpos u elementos del mismo cuerpo.

Con el fin de recuperar la localidad de las operaciones en la radiación y así poder computarla junto con la conducción en una misma operación, se ha introducido aquí una transformación de los datos: Se desprecia la trayectoria de los rayos (que no interactúan con el medio por viajar en el vacío) y se simplifica el modelo a un aporte energético cuerpo a cuerpo o elemento a elemento. Como ventaja adicional la magnitud del aporte energético se separa de la proporción que se esperaría que un cuerpo reciba de otro, permitiendo reutilizar parámetros geométricos en distintos escenarios físicos.

