# Linux Nivel 1

## Tarea 11 - Sustitución de cadenas en Linux

#### El servidor de copia de seguridad en el Stratos DC contiene varios archivos XML de plantilla utilizados por la aplicación Nautilus. Sin embargo, estos archivos XML de plantilla deben ser rellenados con datos válidos antes de que puedan ser utilizados. Una de las tareas diarias de un administrador de sistemas que trabaja en las industrias de xFusionCorp es aplicar comandos de manipulación de cadenas y archivos.

#### Sustituya todas las apariciones de la cadena Random to Echo-Location en el archivo XML /root/nautilus.xml ubicado en el servidor de copia de seguridad.

Para la realizar este ejercicio, vamos a usar directamente el usuario root para no tener que usar el sudo.

Ejecutaremos el comando siguiente

```bash
$ sudo su
```

![comando sudo su](/img/LINUX/LinuxL01/Task11_01_sudo_su.png)

Una vez somos root, vamos a ver el contenido del fichero xml

```
# cat /root/nautilus.xml
```

Como vemos en la etiqueta \<type> aparece la palabra Random que debemos sustituir.

![comando cat](/img/LINUX/LinuxL01/Task11_02_cat.png)

Con el comando siguiente vamos a saber el número de veces que aparece la palabra que estamos buscando.

```
# cat /root/nautilus.xml | grep Random | wc -l
```

Ahora vamos a realizar la sustitución para ellos usamos el comando sed

```
# sed -i 's/Random/Echo-Location/g' /root/nautilus.xml
```

![comando sed](/img/LINUX/LinuxL01/Task11_03_sed.png)

- -i : Opción de edición en el lugar. Quiere decir que los archivos se editan en su lugar sin crear un nuevo archivo.

- s : Es el comando de sustitución

- g : Es una bandera que sustituye globalmente todas las ocurrencias del patrón

Una vez que hemos hecho la sustitución, debemos comprobar que el número de concidencias sea el mismo que el visto anteriormente

```
# cat /root/nautilus.xml | grep Echo-Location | wc -l
```

![comando cat](/img/LINUX/LinuxL01/Task11_04_cat_sed.png)

Ahora que hemos comprobado que el número de coincidencias es el mismo, vamos a ver las 10 primeras líneas del fichero para ver esa sustición

```
# head /root/nautilus.xml
```

![comando head](/img/LINUX/LinuxL01/Task11_05_head.png)
