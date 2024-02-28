# Linux Nivel 1

## Tarea 18 - Límites de Recursos Linux

#### En nuestro servidor de Almacenamiento en el Centro de Datos Stratos estamos teniendo algunos problemas donde el usuario nfsuser está manteniendo cientos de procesos, lo que está degradando el rendimiento del servidor. Por lo tanto, tenemos un requisito para limitar sus procesos máximos. Por favor, establezca sus límites máximos de proceso como se indica a continuación:

#### a. soft limit = 1026

#### b. hard_limit = 2024

Para realizar esta tarea debemos editar el fichero /etc/security/limits.conf como vemos a continuación.

```bash
$ sudo vi /etc/security/limits.conf
```

![sudo vi command](/img/LINUX/LinuxL01/Task18_01_sudo_vi.png)

![add limits](/img/LINUX/LinuxL01/Task18_02_limits_conf.png)
