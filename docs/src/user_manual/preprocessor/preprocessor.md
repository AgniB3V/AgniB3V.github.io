# Preprocesador

## Referencia rápida

Uso general

```
python3 main.py <operación> <directorio>
```

Donde operación define las tareas a realizar  y directorio es la carpeta en donde se buscarán los archivos requeridos.

Ejemplos:

```
python3 main.py process home/usuario/proyectos/satelite
python3 main.py process ./proyectos/satelite
python3 main.py viewm ./proyectos/satelite
python3 main.py viewn ./proyectos/satelite
```



## Estructura de properties.json

El archivo `properties.json` presenta tres secciones principales "global_properties", "materials" y "conditions"


### Propiedades globales

```
"global_properties": {
    "albedo": 0.2,
    "earth_ir": 225.0,
    "solar_constant": 1361.0,
    "initial_temperature": 200.0,
    "element_ray_amount": 5000,
    "earth_ray_amount": 5000,
    "element_max_reflections_amount": 3,
    "orbit_divisions": 15,
    "simulation_time": 86400.0,
    "time_step": 10.0,
    "snap_period": 25.0
}
```

* "albedo": Fracción de la luz solar recibida por la Tierra que es reflejada. Escalar positivo menor a uno.
* "earth_ir": Radiación infrarroja terrestre (\\( \frac{W}{m^2}\\)).
* "solar_constant": Radiación solar (\\( \frac{W}{m^2}\\)).
* "initial_temperature": Temperatura inicial por defecto. Puede ser sobreescrita por las condiciones (\\( K \\)).

* "element_ray_amount" y "earth_ray_amount" establecen la cantidad de rayos a utilizar por elemento para radiación elemento-elemento y elemento-tierra (albedo e ir), respectivamente.
* "element_max_reflection_amount" es el límite de reflexiones  en radiación elemento a elemento.
* "orbit_divisions" establece la cantidad de puntos de la órbita a considerar, aunque es posible que se tomen menos puntos si los puntos de referencia que calcula GMAT se encuentran muy concentrados en algunas secciones.

* "simulation_time": Tiempo total a simular (\\( s \\)).
* "time_step": Intervalo de discretización. Valores más pequeños aumentan la presición, a costa de aumentar el tiempo de cálculo total (\\( s \\)).
* "snap_period": Intervalo de muestreo de resultados. El tiempo total debe ser múltiplo de él (\\( s \\)).


### Materiales

```
"materials": {
    "properties": {
        "materialA": {
            "thermal_conductivity": 0.0,
            "specific_heat": 900.0,
            "density": 2700.0,
            "thickness": 0.05,
            "alpha_sun": 1.0,
            "alpha_ir": 1.0,
       }
       "materialB": { ... }
    },
    "elements": {
        "materialA": [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
        "materialB": [12, 13, 14, 15, 16, 17, 18, 19]
    }
}
```

Se divide en dos subsecciones, siendo la primera "properties", en donde se especifican las caracteristicas físicas de los materiales y la segunda "elements", en donde se indica a través de un arreglo a qué elementos corresponden dichos materiales.

Las propiedades de los materiales son:

- "thermal_conductivity": Conductividad térmica (\\( \frac{W}{m . K}\\)).
- "specific_heat": Calor específico (\\( \frac{J}{kg . K}\\)).
- "density": Densidad (\\( \frac{kg}{m^3}\\)).
- "thickness": Grosor (\\(m\\)).
- "alpha_sun": Absortividad en frecuencias del espectro solar. Escalar positivo menor a uno.
- "alpha_ir": Absortividad en el espectro infrarojo. Escalar positivo menor a uno.

### Conditions
```
"conditions": {
    "properties": {
        "conditionA": {
            "flux_on": true,
            "flux": 100.0,
            "initial_temperature_on": true,
            "initial_temperature": 273.15,
            "two_sides_radiation": true
            "flux": 10.0
       }
    },
    "elements": {
        "conditionA": [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
    }
}
```

Se divide en dos subsecciones, siendo la primera "properties", en donde se especifican las características de las condiciones y la segunda "elements", en donde se indica a través de un arreglo a qué elementos corresponden dichas condiciones.

Las características de una condición son:

- "flux_on": Considerar valor de flujo inicidente. Booleano.
- "flux": Flujo constante incidente (\\( \frac{W}{m^2}\\)).
- "initial_temperature_on": Considerar valor de temperatura inicial. Booleano.
- "initial_temperature": Temperatura inicial del elemento(\\(K\\)).
- "two_sides_radiation": Indica si debe considerarse la orientación del elemento (dirección de su normal según la regla de la mano derecha) al proyectar rayos elemento a elemento.

## Procesamiento de factores de vista

**Archivos necesarios:** `mesh.vtk`, `properties.json`, `ReportFile.txt`, `EclipseLocator.txt`

Calcula factores de vista entre elementos del satélite, Tierra y el Sol.

<center><img src="images/process.png" ...></center>
<center><i> Ejecución de ejemplo de operación process </i></center>

Almacena los resultados en un archivo binario `view_factors.vf`.

## Visualización de materiales

**Archivos necesarios:** `mesh.vtk`, `properties.json`

Muestra en tres dimensiones los materiales asignados a cada elemento sobre el modelo.

<center><img src="images/viewm.png" ...></center>
<center><i> Ejecución de ejemplo de operación viewm </i></center>

## Visualización de orientación de normales

**Archivos necesarios:** `mesh.vtk`

Muestra en tres dimensiones la orientación (dirección de la normal) de cada elemento sobre el modelo.

<center><img src="images/viewn.png" ...></center>
<center><i> Ejecución de ejemplo de operación viewn </i></center>
