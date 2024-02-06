# Solver

El solver fue construido con el objetivo de realizar la simulación de la transferencia de calor del satélite en órbita, frente a la interacción con las fuentes de energía del Sol y la Tierra.

Dado que el rendimiento es un objetivo relevante de este software, se decidió hacer uso de Rust como lenguaje de programación para código a ser ejecutado en CPU, ya que brinda las facilidades de un lenguaje de programación moderno y, adicionalmente, ha demostrado tener tiempos de ejecución comparables a los de C en pruebas realizadas.
Por otro lado, se eligió a OpenCL como lenguaje de programación del código a ser ejecutado en GPU debido a que permite lograr una abstracción completa del hardware subyacente. Esta plataforma es soportada no solo por distintos proveedores de tarjetas gráficas, sino también por distintos tipos de hardware, entre los que se pueden encontrar CPUs y tensores.

Como método numérico para el desarrollo del modelo se eligió FEM (Finite Element Method), debido a su conocida estabilidad numérica frente a geometrías diversas, su abundante bibliografía y por ser el método que usualmente se emplea para el cálculo de este tipo de problemas.
