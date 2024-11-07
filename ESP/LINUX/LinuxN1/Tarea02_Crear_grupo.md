# Linux Nivel 1

## Tarea – Crear un grupo

#### Existen niveles de acceso específicos para usuarios definidos por el equipo de administración del sistema de xFusionCorp Industries.En lugar de proporcionar niveles de acceso a cada usuario individual, el equipo ha decidido crear grupos con niveles de acceso requeridos y agregar usuarios a esos grupos según sea necesario.Vea los siguientes requisitos:

#### - Crear un grupo llamado nautilus_sftp_users en todos los servidores App en Stratos Datacenter.

#### - Añada el usuario stark al grupo nautilus_sftp_users en todos los servidores App. (crear el usuario si no existe).

Lo primero, nos conectaremos a cada uno de los servidores para lanzar los comandos que se indican a continuación.

![Comando ssh](/img/LINUX/LinuxL01/Task02_01_SSH.png)

![Comando ssh](/img/LINUX/LinuxL01/Task02_02_SSH.png)

![Comando ssh](/img/LINUX/LinuxL01/Task02_03_SSH.png)

Haremos uso del comando groupdd precedido de sudo para crear el grupo solicitado.

```bash
$ sudo groupadd nautilus_sftp_users
```

Como vemos, si no lo lanzamos con sudo, fallará.

![Comando groupadd](/img/LINUX/LinuxL01/Task02_04_groupadd.png)

![Comando sudo groupadd](/img/LINUX/LinuxL01/Task02_05_sudo_groupadd.png)

Para verificar que se ha crado el grupo, revisaremos el fichero /etc/group buscando por el nombre del grupo en cuestión, ejecutando el comando siguiente:

```bash
$ cat /etc/group | grep nautilus_sftp_users
```

![Comando cat](/img/LINUX/LinuxL01/Task02_06_cat_etc_group.png)

Ahora, vamos a ver si el usuario stark existe en el sistema. Para ello revisamos el fichero /etc/passwd buscando el nombre del usuario.

```bash
$ cat /etc/passwd | grep stark
```

![Comando cat](/img/LINUX/LinuxL01/Task02_07_cat_etc_passwd.png)

Como vemos, el usuario no existe, por lo que lo añadimos ejecutando el comando useradd precedido de sudo ya que requiere privilegios.

```bash
$ sudo useradd stark
```

```bash
$  cat /etc/passwd | grep stark
```

Tras añadir el usuario, si buscamos éste en /etc/passwd aparece una entrada

![Comando sudo useradd](/img/LINUX/LinuxL01/Task02_08_sudo_useradd.png)

Para añadir el usuario al grupo, usaremos el comando usermod precedido de sudo como se muestra a continuación.

```bash
$  sudo usermod -a -G nautilus_sftp_users stark
```

Opciones usermod usadas:

- -a : Para añadir el usuario al grupo o grupos

- -G : Para especificar el grupo o grupos a los que añadir

Para ver si realmente se ha incluido el usuario en el grupo, tenemos dos opciones, una es ejecutar el comando groups

```bash
$  groups stark
```

La otra, lanzar el comando id

```bash
$  id stark
```

Esta es la salida de la ejecución de los comandos anteriores.

![Comando sudo useradd](/img/LINUX/LinuxL01/Task02_09_sudo_usermod.png)

Como se aprecia en la imagen anterior, laa diferencia entre usar groups o id es que id proporciona mayor información, ya que podemos ver el uid, gid, y los id de los grupos.
