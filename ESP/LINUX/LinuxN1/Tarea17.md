# Linux Nivel 1

## Tarea 17 - Reglas Linux Firewalld

#### El equipo de administradores del sistema Nautilus ha desplegado recientemente una aplicación web UI para su utilidad de copias de seguridad que se ejecuta en el servidor de copias de seguridad Nautilus en el Centro de Datos Stratos. La aplicación se ejecuta en el puerto 8088. Tienen firewalld instalado en ese servidor. Los requisitos que han surgido incluyen los siguientes:

#### Abrir todas las conexiones entrantes en el puerto 8088/tcp. La zona debe ser pública.

Para realizar este ejercicio nos podemos apoyar en la documentación https://firewalld.org/documentation/

Una vez conectados al servidor, nos cambiaremos al usuario root y después veremos el estado del firewall.

```
# systemctl status firewalld
```

![conectarse por ssh, cambiar a root y ejecutar systemctl](/img/LINUX/LinuxL01/Task17_01_ssh.png)

Comprobaremos las zonas de las que disponemos

```
# firewall-cmd --get-zones
```

![ver zonas del FW](/img/LINUX/LinuxL01/Task17_02_firewallcmd.png)

Para crear la regla indicada debemos ejecutar el comando siguiente

```
# firewall-cmd --permanent --zone=public --add-port= 8088/tcp
```

![añadir regla](/img/LINUX/LinuxL01/Task17_03_firewallcmd.png)

Ahora debemos recargar la configuración

```
# firewall-cmd reload
```

![reiniciar FW](/img/LINUX/LinuxL01/Task17_04_firewallcmd.png)

Y por último comprobaremos que se añadió la regla

```
# firewall-cmd --list-ports
```

![ver puertos](/img/LINUX/LinuxL01/Task17_05.png)
