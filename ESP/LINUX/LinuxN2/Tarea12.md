# Linux Nivel 2

## Tarea 12 - Resolución de problemas DNS

#### El equipo de administradores de sistemas de xFusionCorp Industries ha notado problemas intermitentes con la resolución DNS en varias aplicaciones. App Server 2 en Stratos Datacenter está teniendo algunos problemas de resolución DNS, por lo que queremos añadir algunos servidores de nombres DNS adicionales en este servidor.

#### Como solución temporal hemos decidido utilizar el DNS público de Google (ipv4). Por favor, haga los cambios apropiados en este servidor.

Una vez nos hemos conectado al servidor App Server 2 vamos hacer una copia del fichero `/etc/resolv.conf`

Ese fichero contiene los DNS que vamos usar.

```bash
$ sudo cp /etc/resolv.conf /etc/resolv.conf.backup
```

![Copia de backup de fichero resolv.conf](/img/LINUX/LinuxL02/Task12_01_sudo_cp.png)

Una vez tengamos una copia, editamos el fichero y añadimos los DNS de Google (8.8.8.8 y 8.8.4.4)

```bash
$ sudo vi /etc/resolv.conf
```

![Añadir DNS Google](/img/LINUX/LinuxL02/Task12_02_resolvconf.png)

Guardamos y salimos. Y con esto tendríamos realizado el ejercicio.

Si hicieramos un reinicio del servicio de red recibimos un error. No te preocupes, ese error estaba ya presente al iniciar el ejercicio.

```bash
$ sudo systemctl restart network.service
```

![Reiniciar servicio de red](/img/LINUX/LinuxL02/Task12_03_sudo_systemctl_restart.png)

```bash
$ sudo systemctl status network.service
```

![Ver estado del servicio de red](/img/LINUX/LinuxL02/Task12_04_sudo_systemctl_status.png)

Podemos ejecutar el comando indicado, journalctl, que recopila y administra los registros del sistema. Así podemos ver más detalladamente lo que sucede.

```bash
$ sudo journalctl -xe
```

![Revisar error](/img/LINUX/LinuxL02/Task12_05_sudo_journal.png)

Si ejecutamos `ip address` podemos ver si las interfaces están up, como se ve todo está arriba.

![Ver interfaces](/img/LINUX/LinuxL02/Task12_06_ip_address.png)

Si hacemos un `ping` a los servidores DNS de google vemos que estos responden.

![Prueba de conexión](/img/LINUX/LinuxL02/Task12_07_ping.png)
