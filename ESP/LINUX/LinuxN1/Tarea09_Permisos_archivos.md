# Linux Nivel 1

## Tarea 9 - Permisos de Archivos Linux

#### Existen nuevos requerimientos para automatizar un proceso de respaldo que fue realizado manualmente por el equipo de administradores de sistemas de xFusionCorp Industries anteriormente. Para automatizar esta tarea, el equipo ha desarrollado un nuevo script bash xfusioncorp.sh. Ya han copiado la secuencia de comandos en todos los servidores necesarios, sin embargo, no lo hicieron ejecutable en uno de los servidores de aplicaciones es decir, App Server 2 en Stratos Datacenter.

#### Por favor, dar permisos ejecutables a /tmp/xfusioncorp.sh en el servidor de aplicaciones 2. También asegúrese de que todos los usuarios pueden ejecutarlo.

Si hacemos un ls -al sobre el fichero podemos ver que éste no tiene ningún permiso.

```bash
$ ls -al /tmp/xfusioncorp.sh
```

![comando ls](/img/LINUX/LinuxL01/Task09_01_ls_al.png)

Para dar los permisos solicitados, haremos uso del comando chmod seguido de 755 y el fichero en cuestión.

Hacemos uso de 755 para dar los permisos siguientes:

- Al propietario, le damos permiso de lectura (r), escritura (w) y ejecución (x), de ahí el 7

- Al grupo, le damos permiso de lectura (r) y ejecución (x), de ahí el 5

- A otros, le damos permiso de lectura (r) y ejecución (x), de ahí el 5

Estos números es por usar la notiación binaria siguiente:

r (4) w (2) x (1) - 7 es permiso total

r (4) w (2) - 6 permiso lectura - escritura

r(4) x(1) - permiso de lectura y ejecución

Si no recuerdo mal, lo normal es dar permiso de lectura y ejecución y no sólo el de ejecución ya que si no otros no podían ejecutar el .sh de ahí usar la notación 5 en lugar 1.

```bash
$ sudo chmod 755 /tmp/xfusioncorp.sh
```

Para comprobarlo, listamos el fichero

```bash
$ ls -al /tmp/xfusioncorp.sh
```

![comando sudo chmod](/img/LINUX/LinuxL01/Task09_02_sudo_chmod.png)
