# Linux Nivel 1

## Tarea 1 - Crear un usuario

#### Por razones de seguridad, el equipo de seguridad de xFusionCorp Industries ha decidido utilizar usuarios Apache personalizados para cada aplicación web alojada, en lugar de su usuario por defecto. Este será el usuario Apache, por lo que no debería usar el directorio home por defecto. Cree el usuario según los requisitos indicados a continuación:

#### - Crear un usuario llamado john en el servidor de aplicaciones 3 en Stratos Datacenter.

#### - Establezca su UID en 1606 y su directorio de inicio en /var/www/john.

Lo primero que vamos hacer es conectarnos vía SSH con el comando siguiente (RECUERDA: el usuario y el host pueden variar)

```bash
$ ssh banner@172.16.238.12
```

![Comando SSH](/img/LINUX/LinuxL01/Task01_01_SSH.png)

Una vez conectados al servidor, ejecutaremos el siguiente comando

```bash
$ sudo useradd john -d /var/www/john -u 1606
```

Opciones useradd utilizadas:

- -d : Para indicar el path del directorio de inicio

- -u : Para establecer el UID

El comando anterior debemos lanzarlo con sudo ya que requiere tener privilegios, de lo contrario fallará como vemos a continuación.

![Comando useradd](/img/LINUX/LinuxL01/Task01_02_useradd.png)

![Comando sudo useradd](/img/LINUX/LinuxL01/Task01_03_sudo_useradd.png)

Para comprobar que el usuario se ha creado con las opciones correctas, echaremos un vistazo al fichero /etc/passwd

```bash
$ cat /etc/passwd
```

Como podemos ver, se ha creado el usuario con el UID y el directorio solicitados

![Comando cat](/img/LINUX/LinuxL01/Task01_04_cat_etc_passwd.png)
