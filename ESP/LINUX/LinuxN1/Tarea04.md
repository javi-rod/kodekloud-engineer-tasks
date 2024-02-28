# Linux Nivel 1

## Tarea 4 - Usuario Linux sin directorio home

#### El equipo de administradores de sistemas de xFusionCorp Industries ha configurado una nueva herramienta en todos los servidores de aplicaciones, ya que tienen el requisito de crear una cuenta de usuario de servicio que será utilizada por dicha herramienta.

#### Cree un usuario llamado ammar en App Server 2 sin un directorio home.

Vía SSH conectamos con el servidor en cuestión

![Comando ssh](/img/LINUX/LinuxL01/Task04_01_ssh.png)

Una vez conectados, ejecutaremos el comando useradd, ya visto en tareas anteriores, con la opción -M para indicar que el usuario no va a tener directorio home.

```bash
$ sudo useradd -M ammar
```

![Comando sudo useradd](/img/LINUX/LinuxL01/Task04_02_sudo_useradd.png)

Para comprobar que se ha creado el usuario, revisaremos el fichero /etc/passwd buscando por el usuario.

```bash
$ cat /etc/passwd | grep ammar
```

Como podemos ver en el fichero, el usario ha sido creado, pero aparece el home.

![Comando cat](/img/LINUX/LinuxL01/Task04_03_cat_etc_passwd.png)

No hay que preocuparse, si hacemos un listado del directorio /home veremos que para el usuario en cuestión no se ha creado directorio personal.

```bash
$ ls -al /home/
```

![Comando ls](/img/LINUX/LinuxL01/Task04_04_ls_al.png)
