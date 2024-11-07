# Linux Nivel 1

## Tarea 16 - Linux NTP Setup

#### El equipo de administración de sistemas de xFusionCorp Industries ha notado un problema con algunos servidores en el Centro de Datos Stratos donde algunos de los servidores no están sincronizados con la hora. Debido a esto, varias funcionalidades de la aplicación se han visto afectadas. Para solucionar este problema, el equipo ha empezado a utilizar servidores NTP comunes/estándar. Han terminado con la mayoría de los servidores excepto con App Server 2. Por lo tanto, realice las siguientes tareas en este servidor:

#### 1. Instale y configure el servidor NTP en App Server 2.

#### 2. Añada el servidor NTP 1.my.pool.ntp.org en la configuración NTP en App Server 2.

#### 3. **Por favor, no intente iniciar/reiniciar/detener el servicio ntp**, ya que tenemos un reinicio de este servicio programado para esta noche y no queremos que estos cambios se apliquen ahora mismo.

Lo primero que haremos será cambiarnos al usuario root para no usar sudo.

```bash
$ sudo su
```

Ahora vamos a instalar ntp

```
# yum install ntp
```

![comando sudo su](/img/LINUX/LinuxL01/Task16_01_sudo_su.png)

Una vez instalado, lo habilitamos

```
# yum systemctl enable ntpd
```

![comando sytemctl](/img/LINUX/LinuxL01/Task16_02_systemctl.png)

Si vemos el estado, aparece loaded pero inactivo, tal como nos piden.

```
# yum systemctl status ntpd
```

![comando systemctl](/img/LINUX/LinuxL01/Task16_03_systemctl.png)

Para añadir el nuevo servidor, editaremos el fichero /etc/ntp.conf

```
# vi /etc/ntp.conf
```

![comando vi](/img/LINUX/LinuxL01/Task16_04_vi.png)

![editar fichero](/img/LINUX/LinuxL01/Task16_05_vi.png)
