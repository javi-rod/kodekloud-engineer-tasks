# Linux Nivel 2

## Tarea 7 - Instalar un paquete

#### Según los requisitos de la nueva aplicación compartidos por el equipo de desarrollo del proyecto Nautilus, es necesario instalar varios paquetes nuevos en todos los servidores de aplicaciones del centro de datos Stratos. La mayoría de ellos se han completado excepto git.

#### Por lo tanto, instale el paquete git en todos los servidores de aplicaciones.

Tendremos que conectarnos a cada uno de los servidores de aplicaciones. En este caso muestro cómo conectarse al app server 1.

![Conexión ssh al servidor](/img/LINUX/LinuxL02/Task07_01_ssh.png)

Una vez conectados, actualizaremos los paquetes del servidor.

```bash
$ sudo yum update -y
```

![Actualizar paquetes](/img/LINUX/LinuxL02/Task07_02_yum_update.png)

Después de actualizar, vamos a instalar GIT.

```bash
$ sudo  yum install -y git
```

![Instalar GIT](/img/LINUX/LinuxL02/Task07_03_yum_install.png)

Para verifica que se ha instalado, veremos la versión de GIT.

```bash
$ git version
```

![Ver version GIT](/img/LINUX/LinuxL02/Task07_04_git_version.png)
