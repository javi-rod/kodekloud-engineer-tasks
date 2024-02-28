# Linux Nivel 1

## Tarea 3 - Crear un Usuario Linux con shell no interactiva

#### El equipo de Administración de Sistemas de xFusionCorp Industries ha instalado una herramienta de agente de respaldo en todos los servidores de aplicaciones.Según los requerimientos de la herramienta, necesitan crear un usuario con una shell no interactiva.

#### Por lo tanto, cree un usuario llamado anita con una shell no interactiva en el Servidor de aplicaciones 1.

Una vez nos hayamos conectado al servidor requerido, lanzaremos el comando useradd visto anteriormente en la tarea01 con la opción -s para indicar la ruta al shell de inicio de sesión del usuario.

```bash
$ sudo useradd anita -s /sbin/nologin
```

![Comando sudo useradd](/img/LINUX/LinuxL01/Task03_01_sudo_useradd.png)

Para comprobar que todo fue bien, revisaremos si en /etc/passwd la usuaria tiene como shell el valor indicado anteriormente.

```bash
$ cat /etc/passwd | grep anita
```

![Comando cat](/img/LINUX/LinuxL01/Task03_02_cat_etc_passwd.png)
