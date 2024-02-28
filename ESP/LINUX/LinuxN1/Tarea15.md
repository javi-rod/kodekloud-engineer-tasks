# Linux Nivel 1

## Tarea 15 - Configuración de las Zonas Horarias de Linux

#### Durante la puesta en marcha diaria, se ha detectado que la zona horaria de los servidores de aplicaciones Nautilus en el centro de datos Stratos no coincide con la zona horaria del centro de datos local, que es Asia/Kathmandu.

#### Corrija el desajuste.

Si ejecutamos el comando siguiente veremos que efectivamente la zona horaria no es la que solicitan.

```bash
$ timedatectl
```

![comando timedatectl](/img/LINUX/LinuxL01/Task15_01_timedatectl.png)

Para saber qué zonas horarias tenemos en Asia podemos lanzar el comando siguiente

```bash
$ timedatectl list-timezones | grep Asia
```

![comando timedatectl](/img/LINUX/LinuxL01/Task15_02_timedatectl.png)

Para establecer un nueva zona, ejecutaremos el comando siguiente

```bash
$ sudo timedatectl set-timezone Asia/Kathmandu
```

![comando timedatectl](/img/LINUX/LinuxL01/Task15_03_timedatectl.png)

Si lanzamos de nuevo el comando timedatectl veremos que la zona horaria se ha modificado.

```bash
$ timedatectl
```

![comando timedatectl](/img/LINUX/LinuxL01/Task15_04_timedatectl.png)
