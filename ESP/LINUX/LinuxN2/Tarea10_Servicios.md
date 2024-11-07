# Linux Nivel 2

## Tarea 10 - Servicios Linux

#### Según los detalles compartidos por el equipo de desarrollo, la nueva versión de la aplicación tiene algunas dependencias en el back-end. Hay algunos paquetes/servicios que necesitan ser instalados en todos los servidores de aplicaciones bajo Stratos Datacenter. De acuerdo a los requerimientos por favor realice los siguientes pasos:

#### a. Instale el paquete squid en todos los servidores de aplicaciones.

#### b. Una vez instalado, asegúrese de que está habilitado para iniciar durante el arranque.

Los siguientes pasos debemos ejecutarlos en cada uno de los servidores, una vez nos hayamos conectado vía SSH.

Lo primero, nos cambiaremos al usuario root, evitando usar el sudo para cada instrucción.

```bash
$ sudo su
```

![Cambiar a usuario root](/img/LINUX/LinuxL02/Task10_01_sudo_su.png)

A continuación actualizaremos los paquetes ya instalados.

```
# yum update -y
```

![Actualizar paquetes](/img/LINUX/LinuxL02/Task10_02_yum_update.png)

Después instalaremos squid.

```
# yum install squid -y
```

![Instalar squid](/img/LINUX/LinuxL02/Task10_03_yum_install.png)

Ahora que ya tenemos instalado squid, vamos a ver el estado del servicio.

```
# systemctl status squid
```

![Estado servicio squid](/img/LINUX/LinuxL02/Task10_04_yum_status.png)

Como vemos no está iniciado, por lo que ejecutaremos los comandos siguientes para arrancar el servicio y comprobar el estado.

```
# systemctl start squid

# systemctl status squid
```

![Arrancar servicio squid](/img/LINUX/LinuxL02/Task10_05_yum_start.png)

Como vemos en la imagen anterior, el servicio está iniciado, pero "disabled". Para habilitarlo ejecutaremos el comando siguiente.

```
# systemctl enable squid
```

![Habilitar squid](/img/LINUX/LinuxL02/Task10_06_yum_enable.png)
