# Solver

## Ejecución
En caso de querer ejecutar el Solver por fuera de la GUI, se debe ejecutar el siguiente comando:

```
./target/release/solver <directory> <method>
```

Siendo directory el directorio donde se encuentran los archivos necesarios, mientras que method debe ser uno de los siguientes: Implicit o GPU

Los archivos necesarios para ejecutar el solver son: mesh.vtk, properties.json y view_factors.vf.

Ejemplo ejecución Implicito:

INSERTAR IMAGEN

Ejemplo ejecución GPU:

INSERTAR IMAGEN

Una vez ejecutado, genera una carpeta results que contiene un archivo result.vtk.series y un archivo result\<i\>.vtk por cada instante de la simulación. 

## Parámetros

Los parámetros necesarios para ejecutar el solver que se encuentran en el properties.json son los siguientes:

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

- "orbital_period" indica el periodo de la orbita, es generado por el preprocesador
- "albedo" es el factor de albedo
- "earth_ir" es el flujo de calor proveniente por la radiación IR de la tierra, se mide en $\frac{W}{m^2}$
- "solar_constant" es la constante de flujo solar, se mide en $\frac{W}{m^2}$
- "simulation_time" es el tiempo de simulación expresado en segundos
- "time_step" es el paso de tiempo que usara la simulación, esta expresado en segundos
- "snap_perior" indica cada cuanto tiempo se guardara un resultado, esta expresado en segundos
- "orbit_divisions" es la cantidad de divisiones en la orbita para los factores de vista
- "eclipse_start" indica cuando empieza el eclipse, es generado por el preprocesador
- "eclipse_end" indica cuando termina el eclipse, es generado por el preprocesador

Es importante aclarar que es posible volver a correr el solver sin necesidad de volver a correr el preprocesador en caso de quererse cambiar algun parámetro, lo cual ahorraria bastante tiempo, sin embargo, esto no es posible si se modifica alguno de estos parametros: "orbital_period", "orbit_divisions", "eclipse_start", "eclipse_end". Tampoco es posible si se modifica cualquier otro parametro dentro de global properties no indicado aqui (por ejemplo los que se usan como entrada del preprocesador).

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

Se divide en dos subsecciones. "elements", en donde se indica un array con los ids de los elementos a los que correspondenen y "properties", donde se especifican las características físicas de los materiales:

- "thermal_conductivity": Conductividad térmica ($\frac{W}{m.K}$).
- "specific_heat": Calor específico ($\frac{J}{kg.K}$).
- "density": Densidad ($\frac{kg}{m^3}$).
- "thickness": Grosor (m).
- "alpha_sun": Absorptividad en frecuencias del espectro solar. Escalar positivo menor a uno.
- "alpha_ir": Absorptividad en el espectro infrarojo. Escalar positivo menor a uno.

De los anteriores, en caso de querer volver a ejecutar el solver sin reejecutar el preprocesador, no se pueden modificar "alpha_sun" y "alpha_ir".

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

Se divide en dos subsecciones. "elements", en donde se indica un array con los ids de los elementos a los que correspondenen y "properties", donde se especifican las condiciones específicas:

- "flux_on": Indica si se debe considerar el valor del parametro "flux"
- "flux": Flujo constante incidente ($\frac{W}{m^2}$).
- "initial_temperature_on": Indica si se debe considerar el valor del parametro "initital_temperature"
- "initial_temperature": Temperatura inicial (K).
- "two_sides_radiation": Indica si los elementos emiten radiación hacia ambos lados.

De los anteriores, en caso de querer volver a ejecutar el solver sin reejecutar el preprocesador, no se puede modificar "two_sides_radiation"


## Tiempo de ejecución vs Precisión

La modificación de los distintos parámetros en general implica un tradeoff entre el tiempo de ejecución y precisión, a continuación se explica como afecta la modificación de cada parametro.

- "simulation_time": En caso de aumentar aumenta el tiempo de ejecución

- "time_step": Cuanto mas chico mejor precisión pero mayor tiempo de ejecución.

- "snap_period": Cuanto mas chico mayor tiempo de ejecución, principalmente en modo GPU.

- "orbit_divisions": Cuanto mas grande habrá un leve aumento del tiempo de ejecución.

- Cantidad de elementos: Cuanto mayor sea, más aumentan el tiempo de ejecución y la precisión.

El resto de parámetros no afectan el tiempo de ejecución ni la precisión.