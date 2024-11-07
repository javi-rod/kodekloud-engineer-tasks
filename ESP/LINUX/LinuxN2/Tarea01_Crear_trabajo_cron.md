# Linux Nivel 2

## Tarea 1 - Crear un trabajo en Cron

#### El equipo de administradores del sistema Nautilus ha preparado scripts para automatizar varias tareas diarias. Quieren que se desplieguen en todos los servidores de aplicaciones en Stratos DC en un horario establecido. Antes de eso, necesitan probar una funcionalidad similar con un cron job de ejemplo. Por lo tanto, realice los siguientes pasos:

#### a. Instale el paquete cronie en todos los servidores de aplicaciones Nautilus e inicie el servicio crond.

#### b. Añada un cron \*/5 \* \* \* \* echo hello > /tmp/cron_text para el usuario root.

Nos conectaremos a los 3 servidores de aplicaciones con el comando ssh usuario@ip como vemos en las capturas siguientes.

![Conexión SSH Nautilus App 1 ](/img/LINUX/LinuxL02/Task01_01_ssh.png)

![Conexión SSH Nautilus App 2](/img/LINUX/LinuxL02/Task01_02_ssh.png)

![Conexión SSH Nautilus App 3](/img/LINUX/LinuxL02/Task01_03_ssh.png)

Una vez conectados a cada uno de los servidores, lanzaremos los comandos siguientes.

Primero, vamos a instalar el paquete cronie que nos indican.

```bash
$ sudo yum install cronie
```

![Instalar paquete cronie](/img/LINUX/LinuxL02/Task01_04_sudo_yum_install_cronie.png)

Una vez instalado, vamos iniciar el servicio

```bash
$ sudo systemctl start crond
```

![Arrancar servicio crond](/img/LINUX/LinuxL02/Task01_05_sudo_systemctl_start_crond.png)

Como vemos nos da un Warning. Tenemos que ejecutar el comando indicado, para recargar la configuración del administrador de systemd. Entre otras cosas el comando recarga todos los archivos de unidad, que es precisamente lo que nos advierte que ha cambiado.

```bash
 $ sudo systemctl daemon-reload
```

![Recargar configuración](/img/LINUX/LinuxL02/Task01_06_sudo_systemctl_daemon_reload.png)

Para ver que el servicio está up lanzamos el comando siguiente

```bash
$ sudo systemctl status crond
```

![Estado servicio crond](/img/LINUX/LinuxL02/Task01_07_sudo_systemctl_status_crond.png)

Una vez comprobado que está arrancado vamos a editar el fichero /etc/crontab. Previamente nos cambiaremos al usuario root.

```bash
$ sudo su
```

![Elevar privilegios cambiando a root](/img/LINUX/LinuxL02/Task01_08_sudo_su.png)

```
# vi /etc/crontab
```

![Editar con vi crontab](/img/LINUX/LinuxL02/Task01_09_vi_etc_crontab.png)

Añadimos la línea indicada en el apartado b y salimos y guardamos.

![Añadir el job](/img/LINUX/LinuxL02/Task01_10_edit_crontab.png)

Si comprobamos, de nuevo, el contenido de /etc/crontab veremos la línea añadida.

![Visualizar crontab](/img/LINUX/LinuxL02/Task01_11_cat_crontab.png)

Otra forma para editar el crontab sería ejecutando el siguiente comando.

```
# crontab -e
```

![Editar crontab](/img/LINUX/LinuxL02/Task01_12_crontab_e.png)

Añadimos la línea indicada y guardamos y cerramos.

![Añadimos job](/img/LINUX/LinuxL02/Task01_13_edit_crontab.png)

Vemos que una vez editado el fichero nos aparece un mensaje indicando que no hay crontab para el usuario root y se ha usado uno vacío.

![Info sobre que no existe crontab para el root](/img/LINUX/LinuxL02/Task01_14_crontab_info.png)

Si comprobamos el fichero /etc/crontab vemos que la línea no se ha añadido

![Comprobar contenido de crontab](/img/LINUX/LinuxL02/Task01_15_cat_crontab.png)

El motivo es el siguiente:

El comando crontab -e y el archivo /etc/crontab son dos formas diferentes de gestionar las tareas de cron, y no se sincronizan entre sí.

Cuando usamos crontab -e, estamos editando una tabla de cron específica para el usuario actual. Estas tablas de cron de usuario se almacenan en un lugar diferente (normalmente en /var/spool/cron/crontabs/) y no afectan al archivo /etc/crontab.

Por otro lado, el archivo /etc/crontab es una tabla de cron del sistema que puede contener trabajos de cron para varios usuarios. Este archivo es gestionado directamente y no se ve afectado por los comandos crontab -e de los usuarios individuales.

Por lo tanto, al añadir una tarea usando crontab -e como el usuario root, no vemos esa tarea en el archivo /etc/crontab porque son gestionados de forma independiente.

Si hacemos un cat al directorio /var/spool/cron/root sí vemos la línea añadida.

![Visualizar contenido de /var/spool/cron/root ](/img/LINUX/LinuxL02/Task01_16_cat_var_spool_cron_root.png)
