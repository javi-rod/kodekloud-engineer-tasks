# Linux Nivel 1

## Tarea 19 - Instalación de Selinux

#### El equipo de seguridad de xFusionCorp Industries realizó recientemente una auditoría de seguridad de su infraestructura y propuso ideas para mejorar la seguridad de las aplicaciones y los servidores. Decidieron utilizar SElinux para una capa de seguridad adicional. Todavía están planeando cómo lo implementarán; sin embargo, han decidido empezar a hacer pruebas con servidores de aplicaciones, así que basándose en las recomendaciones tienen los siguientes requisitos:

#### Instalar los paquetes requeridos de SElinux en el servidor de aplicaciones 3 en el Centro de Datos Stratos y deshabilitarlo permanentemente por ahora; será habilitado después de hacer algunos cambios de configuración requeridos en este host. No se preocupe por reiniciar el servidor ya que ya hay un reinicio programado para la ventana de mantenimiento de esta noche. También ignore el estado de la línea de comandos SElinux en este momento; el estado final después del reinicio debe ser **deshabilitado**

Primero nos cambiaremos a root

```bash
$ sudo su
```

![sudo su command](/img/LINUX/LinuxL01/Task19_01_sudo_su.png)

Actualizamos los paquetes instalados

```
# yum update
```

![yum update command](/img/LINUX/LinuxL01/Task19_02_yum_update.png)

Una vez que terminemos, pasaremos a instalar los paquetes necesarios para SELinux

```
# yum install policycoreutils selinux-policy selinux-policy-targeted
```

![yum install command](/img/LINUX/LinuxL01/Task19_03_yum_install.png)

Cuando haya terminado podremos ver el estado de SELinux

```
# sestatus
```

Como vemos nos aparece como disabled. Ese es el estado actual.

![sestatus command](/img/LINUX/LinuxL01/Task19_04_sestatus.png)

Para ver su configuración debemos revisar el fichero /etc/selinux/config

```
vi /etc/selinux/config
```

Como vemos SELINUX está en enforcing y nos piden dejarlo deshabilitado. Demos cambiarlo por disabled y guardarlo.

![edit selinux config](/img/LINUX/LinuxL01/Task19_05_selinux_conf.png)
