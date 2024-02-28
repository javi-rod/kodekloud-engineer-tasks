# Linux Nivel 1

## Tarea 14 - Linux - Run Levels

#### Se han instalado nuevas herramientas en los servidores de aplicaciones del Centro de Datos Stratos. Algunas de estas herramientas sólo se pueden gestionar desde la interfaz gráfica de usuario. Por lo tanto, hay algunos requisitos para estos servidores de aplicaciones como a continuación.

#### En todos los servidores de aplicaciones en Stratos Datacenter, cambiar el runlevel por defecto para que puedan arrancar en GUI (interfaz gráfica de usuario) por defecto. **Por favor, no intente reiniciar estos servidores después de completar esta tarea.**

Runlevels es usado en sysV init mientras que en systemd init son systemd targets

Para saber si nuestro sistema usa sysV init o systemd init ejecutaremos el comando siguiente

```bash
$ ls -l /sbin/init
```

Como podemos ver, nuestro sistema hace uso de systemd

![comando ls](/img/LINUX/LinuxL01/Task14_01_ls.png)

Si ejecutamos el comando runlevel veremos nos devuelve un número.

```bash
$ runlevel
```

![comando runlevel](/img/LINUX/LinuxL01/Task14_02_runlevel.png)

Ese runlevel 3 nos indica que actualmente se está ejecutando en línea de comando.

Como estamos en systemd init se usa systemd targets y para ver cual se está usando en el arranque por defecto debemos ejecutar

```bash
$ systemctl get-default
```

![comando systemctl](/img/LINUX/LinuxL01/Task14_03_systemctl.png)

multi-user.target quiere decir que arranca en módo línea de comandos.

Para modificarlo debemos cambiarlo por graphical.target como se indica a continuación.

```bash
$ sudo systemctl set-default graphical.target
```

![comando systemctl](/img/LINUX/LinuxL01/Task14_04_systemctl.png)

Si volvemos a comprobar que systemd target está ahora configurado por defecto, veremos que ha cambiado, ahora arrancará en modo gráfico.

```bash
$ systemctl get-default
```

![comando systemctl](/img/LINUX/LinuxL01/Task14_05_systemctl.png)
