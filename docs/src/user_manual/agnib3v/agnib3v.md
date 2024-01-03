# Agni B3V

Agni B3V es un paquete de herramientas diseñado para facilitar la realización de análisis térmico satelital desde el diseño del modelo hasta la visualización de resultados. Dichas herramientas son:

- [Graphical User Interface](/user_manual/gui/gui.md): Se ofrece una herramienta gráfica para la creación de proyectos y la utilización de las distintas herramientas del paquete.
- [FreeCAD](/user_manual/freecad/freecad.md): FreeCAD es una aplicación libre de diseño asistido por computadora. Es la aplicación recomendada para el desarrollo de modelos ya que permite una fácil integración con el paquete proporcionado. Para más información, visitar https://www.freecad.org/.
- [FreeCAD (Thermal B3V Addon)](/user_manual/freecad_addon/freecad_addon.md): Thermal B3V ofrece un addon que añade un nuevo workbench, el cual facilita la utilización de las distintas herramientas del paquete a través de la interfaz gráfica proporcionada por FreeCAD.
- [GMAT](/user_manual/gmat/gmat.md):
- [Preprocessor](/user_manual/preprocessor/preprocessor.md):
- [Solver](/user_manual/solver/solver.md): Herramienta que permite la realización de la simulación térmica. Puede utilizarse tanto en CPU como GPU.
- [Paraview](/user_manual/paraview/paraview.md): Es una software de codigo abierto que permite la visualización de los resultados a través del tiempo en un gráfico 3D del modelo.
- [Plotter](/user_manual/plotter/plotter.md): Herramienta que permite visualizar los resultados en graficos de temperatura vs tiempo.

Cada una de estas herramientas pueden ser utilizadas de manera independiente o en conjunta a través de la GUI.

Este trabajo fue realizado bajo el marco del Trabajo Profesional de Ingeniería Informática de la Univesidad de Buenos Aires.

El equipo que realizo este proyecto esta formado por:

- Barreneche Franco
- Belinche Gianluca
- Botta Guido
- Ventura Julian

Se deja a discreción del usuario la correctitud de los resultados generados por el presente software.

Dicho esto, a continuación se presentan las limitaciones actuales del mismo:

- Solo se permiten orbitas circulares
- La aptitud del satélite solo puede ser Sun Pointing
- El albedo presenta un error mayor al de las demás interacciones, por lo que se debe tener especial atención en simulaciones donde este sea el componente principal. 
