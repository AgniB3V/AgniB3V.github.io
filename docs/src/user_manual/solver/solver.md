# Solver

## Ejecución

En caso de querer ejecutar el Solver por fuera de la GUI, se debe ejecutar el siguiente comando:

```
./target/release/solver <directory> <method>
```

Siendo `<directory>` el directorio donde se encuentran los archivos necesarios, mientras que `<method>` debe tomar el valor de "Implicit" o el de "GPU"

Los archivos necesarios para ejecutar el solver son: `mesh.vtk`, `properties.json` y `view_factors.vf`.

Una vez ejecutado, genera una carpeta results que contiene un archivo `result.vtk.series` y un archivo `result<i>.vtk` por cada instante de la simulación.

## Parámetros

Los parámetros necesarios para ejecutar el solver que se encuentran en el `properties.json` son los siguientes:

### Global Properties

```
"global_properties": {
    "orbital_period": 5828.516639879384,
    "albedo": 0.2,
    "earth_ir": 225.0,
    "solar_constant": 1361.0,
    "initial_temperature": 293.15,
    "simulation_time": 175000.0,
    "time_step": 10.0,
    "snap_period": 100.0,
    "orbit_divisions": 60,
    "eclipse_start": 603.2083601206168,
    "eclipse_end": 2646.8503601206166
}
```

- `orbital_period`: Indica el periodo de la orbita, es generado por el preprocesador.
- `albedo`: Factor de albedo.
- `earth_ir`: Flujo de calor proveniente por la radiación IR de la tierra \\([\frac{W}{m^2}]\\).
- `solar_constant`: Constante de flujo solar \\([\frac{W}{m^2}]\\).
- `simulation_time`: Tiempo de simulación expresado en segundos.
- `time_step`: Paso de tiempo que usara la simulación, esta expresado en segundos.
- `snap_perior`: Indica cada cuanto tiempo se guardara un resultado, esta expresado en segundos.
- `orbit_divisions`: Cantidad de divisiones en la orbita para los factores de vista.
- `eclipse_start`: Indica cuando empieza el eclipse, es generado por el preprocesador.
- `eclipse_end`: Indica cuando termina el eclipse, es generado por el preprocesador.


Los parámetros `albedo`, `earth_ir`, `solar_constant`, `initial_temperature`, `simulation_time`, `time_step` y `snap_period` pueden ser alterados manualmente para 
modificar las caracteristicas de la simulación sin necesidad de volver a ejecutar el preprocesador, lo que disminuye el tiempo total empleado. 
Una modificación en cualquiera de los parámetros restantes requiere volver a ejecutar el preprocesador para el correcto funcionamiento de la simulación.


### Materials

```
"materials": {
    "properties": {
        "aluminio": {
            "thermal_conductivity": 237.0,
            "specific_heat": 900.0,
            "density": 2700.0,
            "thickness": 0.05,
            "alpha_sun": 1.0,
            "alpha_ir": 1.0,
            "name": "aluminio"
        }
    },
    "elements": {
        "aluminio": [1,2,3,4,5,6,7,8]
    }
}
```

Se divide en dos subsecciones, siendo la primera "properties", en donde se especifican las caracteristicas físicas de los materiales y la segunda "elements", en donde se indica a través de un arreglo a qué elementos corresponden dichos materiales.

Las propiedades de los materiales son:

- `thermal_conductivity`: Conductividad térmica \\([\frac{W}{m \ K}]\\).
- `specific_heat`: Calor específico \\([\frac{J}{kg \ K}]\\).
- `density`: Densidad \\([\frac{kg}{m^3}]\\).
- `thickness`: Grosor \\([m]\\).
- `alpha_sun`: Absortividad en frecuencias del espectro solar. Escalar positivo menor a uno.
- `alpha_ir`: Absortividad en el espectro infrarojo. Escalar positivo menor a uno.


Los parámetros `thermal_conductivity`, `specific_heat`, `density` y `thickness` pueden ser alterados manualmente sin necesidad de volver a ejecutar el preprocesador. 


### Conditions

```
"conditions": {
    "elements": {
        "hot_temperature": [
            1,2,3,4
        ]
    },
    "properties": {
        "hot_temperature": {
            "initial_temperature_on": true,
            "initial_temperature": 573.0,
            "flux_on": false,
            "flux": 0.0,
            "two_sides_radiation": false
        }
    }
}
```

Se divide en dos subsecciones, siendo la primera "properties", en donde se especifican las características de las condiciones y la segunda "elements", en donde se indica a través de un arreglo a qué elementos corresponden dichas condiciones.

Las características de una condición son:

- `flux_on`: Indica si se debe considerar el valor del parametro `flux`
- `flux`: Flujo constante incidente (\\(\frac{W}{m^2}\\)).
- `initial_temperature_on`: Indica si se debe considerar el valor del parametro `initital_temperature`
- `initial_temperature`: Temperatura inicial (\\(W\\)).
- `two_sides_radiation`: Indica si los elementos emiten radiación hacia ambos lados.

Los parámetros `flux_on`, `flux`, `initial_temperature_on` e `initial_temperature` pueden ser alterados manualmente sin necesidad de volver a ejecutar el preprocesador. 

## Tiempo de ejecución vs Precisión

La modificación de los distintos parámetros implica, en general, un tradeoff entre el tiempo de ejecución y precisión. Aquellos parámetros que tienen impácto en alguna de estas dos variables son:

- `simulation_time`: Al aumentar, incrementa el tiempo de ejecución.

- `time_step`: Al disminuir, mejora la precisión de la simulación,  a costa de un mayor tiempo de ejecución.

- `snap_period`: Al disminuir, mejor será la resolución de datos extraidos de la simulación, a costa de un mayor tiempo de ejecución.

- `orbit_divisions`: Al aumentar, mejor será la discretización de la órbita y con ello la precisión de la simulación, a costa de un mayor tiempo de ejecución.

- Cantidad de elementos en malla: Al aumentar, mejor será la discretización del modelo y con ello la precisión de la simulación, a costa de un mayor tiempo de ejecución.

