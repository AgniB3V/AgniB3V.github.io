# Instalación

Se provee un instalador para el software, el cual puede ser encontrado en el [último release](https://github.com/JulianVentura/TrabajoProfesional/releases) del repositorio del proyecto. Este software fue probado para el sistema operativo Ubuntu 22.04 LTS.

Para realizar la instalación, descargar el archivo `AgniB3V.-.v1.0.0.zip` y moverlo al directorio deseado. Hacer click derecho sobre alguna región vacía del directorio actual y elegir la opción _"Abrir en una terminal"_.
En la terminal, escribir uno a uno los siguientes comandos:

```bash
unzip AgniB3V.-.v1.0.0.zip -d Agni
cd Agni
sh install
```

Tras haber finalizado la instalación, se podrá iniciar AgniB3V haciendo click derecho sobre el archivo `AgniB3V` y seleccionando _"Ejecutar como Programa"_.

## Errores conocidos

Si se experimentan errores al momento de ejecutar el solver, puede seguir las siguientes instrucciones:

En primer lugar, asegurese de contar con los últimos drivers instalados para su proveedor de tarjeta gráfica. Obtenga los drivers para [AMD](https://www.amd.com/es/support) o [Nvidia](https://la.nvidia.com/Download/index.aspx) de fuentes oficiales.

Si los problemas persisten, puede que requiera proveer permisos de administrador a AgniB3V. Para esto deberá ejecutar el archivo `AgniB3V-root` e ingresar la contraseña del usuario administrador cuando le sea solicitado.
