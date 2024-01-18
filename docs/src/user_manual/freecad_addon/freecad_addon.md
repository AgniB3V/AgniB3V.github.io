# Agni Addon

Para facilitar el uso de las herramientas que permiten realizar y visualizar una simulación térmica satelital, se ofrece un addon para FreeCAD. Este agrega un nuevo workbench, cuyo uso se detallará a continuación.

<center><img src="images/addon1.png" ...></center>
<center><i></i></center>

## Prerrequisito

Para la utilización completa del workbench, es necesario haber creado un modelo con anterioridad. Si aún no completó este paso, vaya a la sección de [Modelado](../freecad_model/freecad_model.md).

## Creación de Mallado FEM

Para la creación de un mallado FEM, se debe seleccionar el objeto del modelo y presionar en el botón del mallado, como se ve a continuación:

<center><img src="images/addon2.png" ...></center>
<center><i></i></center>

Esto generará automáticamente una malla de triángulos bidimensionales de primer orden, tal cual requiere el sistema para funcionar correctamente. La malla se creará bajo el grupo "Analysis" con el nombre "\<nombre_objeto\>_Mesh", en este caso "BooleanFragments_Mesh".

<center><img src="images/addon3.png" ...></center>
<center><i></i></center>

Si hacemos doble click en el objeto de la malla, se abrira un cuadro el cual permite editar el tamaño máximo y mínimo de elemento. En caso de cambiar uno de estos parámetros, se debe recrear la malla presionando el botón "Apply".

Es importante no cambiar los valores de "Element dimension" y "Element order" para garantizar el correcto funcionamiento del sistema.

<center><img src="images/addon4.png" ...></center>
<center><i></i></center>

### Regiones

Es posible crear regiones para darle un mayor o menor detalle a las distintas superficies o sólidos del modelo. Para ello, se debe presionar el botón de creación de regiones, como se indica a continuación:

<center><img src="images/addon5.png" ...></center>
<center><i></i></center>

La región se creará bajo el grupo de la malla, con el nombre de "MeshRegion" o "MeshRegionNNN" si hay más de una región. 

<center><img src="images/addon7.png" ...></center>
<center><i></i></center>

Al hacer doble click sobre la región creada se abrirá un cuadro el cual permite editar el máximo tamaño de elemento y sobre qué región queremos aplicar esta restricción.

<center><img src="images/addon6.png" ...></center>
<center><i></i></center>

Una vez aplicada la restricción, se debe apretar "OK", volver a abrir el cuadro de y apretar el botón de "Apply" para regenerar la malla con la nueva restricción.

<center><img src="images/addon8.png" ...></center>
<center><i></i></center>

Como podemos ver a continuación, se regeneró la malla con un detalle mucho mayor sobre la región restringida.

<center><img src="images/addon9.png" ...></center>
<center><i></i></center>

## Definición de Propiedades Globales

TODO

## Asignación de Materiales

Para crear un nuevo material, se debe presionar el botón de edición de materiales, como se muestra a continuación:

<center><img src="images/addon10.png" ...></center>
<center><i></i></center>

Esto abrirá una ventana con el editor de materiales, en el cual se debe presionar "Add Material" para agregar un nuevo material.

<center><img src="images/addon11.png" ...></center>
<center><i></i></center>

Se debe poner un nombre, "Aluminio" en este caso, y presionar "OK".

<center><img src="images/addon12.png" ...></center>
<center><i></i></center>

Esto creara el nuevo material, el cual se puede editar presionando sobre el mismo.

<center><img src="images/addon13.png" ...></center>
<center><i></i></center>

Una vez creado, aparecerá en el panel del modelado con el nombre elegido, bajo el grupo de "\_MATERIALS\_"

<center><img src="images/addon14.png" ...></center>
<center><i></i></center>

Finalmente, para asignar el material, se debe hacer doble click en el objeto del material en el panel "Model". Esto abrirá un cuadro en el que se podrá asignar el material tanto a solidos como a caras.

No se deben asignar materiales a ejes, ya que este no es soportado por el sistema y romperá al momento de la exportación del mallado y propiedades.

<center><img src="images/addon15.png" ...></center>
<center><i></i></center>

## Asignación de Condiciones

TODO

## Exportación del Mallado y Propiedades

TODO
