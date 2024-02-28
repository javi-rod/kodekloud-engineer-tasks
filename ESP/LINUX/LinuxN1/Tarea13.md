# Linux Nivel 1

## Tarea 13 - Cron programar denegar a los usuarios

#### Para cumplir con las normas de seguridad, el equipo del proyecto Nautilus ha decidido aplicar algunas restricciones en el acceso a crontab para que sólo los usuarios autorizados puedan crear/actualizar las tareas cron. Limitar el acceso a crontab a los usuarios especificados a continuación en App Server 3.

#### Permitir el acceso a crontab al usuario john y denegar el mismo acceso al usuario eric.

Para pemitir o denegar el acceso se necesitan dos ficheros, cron.allow y cron.deny dentro del directoro /etc.

Lo primero comprobaremos si esos ficheros existen, para lo que listaremos el contenido en /etc que empiece con cron.

```bash
$ ls -al /etc/cron*
```

![comando ls](/img/LINUX/LinuxL01/Task13_01_ls.png)

Como vemos los dos ficheros no existen, por tanto los crearemos de la forma siguiente

```bash
$ sudo vi /etc/cron.allow
```

En este fichero añadiremos al usuario que debe tener permiso, en este caso john

![comando sudo vi](/img/LINUX/LinuxL01/Task13_02_sudo_vi.png)

![editor vi](/img/LINUX/LinuxL01/Task13_03_vi.png)

```bash
$ sudo vi /etc/cron.deny
```

En este fichero añadiremos al usuario que no debe tener permiso, en este caso eric.

![comando sudo vi](/img/LINUX/LinuxL01/Task13_04_sudo_vi.png)

![editor vi](/img/LINUX/LinuxL01/Task13_05_vi.png)

Una vez creados esos ficheros con los usuarios, si hacemos un listado como el anterior citado veremos que ya están presentes ambos ficheros.

```bash
$ ls -al /etc/cron*
```

![comando ls](/img/LINUX/LinuxL01/Task13_06_ls.png)

Ahora reiniciamos el servicio

```bash
$ sudo systemctl restart crond.service
```

Comprobamos que esté running

```bash
$ sudo systemctl status crond.service
```

![comando sudo systemctl](/img/LINUX/LinuxL01/Task13_07_sudo_systemctl.png)

Si ahora revisamos los permisos vemos que sale que john no tiene permiso.

![comando sudo crontab](/img/LINUX/LinuxL01/Task13_08_sudo_crontab.png)

Lo anterior es debido a que no hay ningún archivo crontab, no hay tareas cron para el usuario.
