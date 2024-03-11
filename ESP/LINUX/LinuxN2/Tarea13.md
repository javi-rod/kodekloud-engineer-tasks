# Linux Nivel 2

## Tarea 13 - Configuración de Firewalld en Linux

#### Para asegurar nuestra infraestructura Nautilus en Stratos Datacenter hemos decidido instalar y configurar firewalld en todos los servidores de aplicaciones. Tenemos servicios Apache y Nginx ejecutándose en estas aplicaciones. Nginx se ejecuta como un servidor proxy inverso para Apache. Podríamos tener configuraciones de firewall más robustas en el futuro, pero por ahora hemos decidido ir con los requisitos que se enumeran a continuación:

#### a. Permitir todas las conexiones entrantes en el puerto Nginx, es decir, 80.

#### b. Bloquear todas las conexiones entrantes en el puerto de Apache, es decir 8080.

#### c. Todas las reglas deben ser permanentes.

#### d. La zona debe ser pública.

#### e. Si los servicios Apache o Nginx no se están ejecutando, asegúrese de iniciarlos.

En cada uno de los servidores deberemos realizar los pasos siguientes.

Lo primero, actualizar paquetes.

```bash
$ sudo yum update -y
```

![Actualizar paquetes](/img/LINUX/LinuxL02/Task13_01_update.png)

Una vez actualizados, procedemos a instalar `firewalld`

```bash
$ sudo yum install -y firewalld
```

![Instalar firewalld](/img/LINUX/LinuxL02/Task13_02_install_firewalld.png)

Terminado de instalar, veremos el estado del servicio.

```bash
$ systemctl status firewalld
```

![Estado firewalld](/img/LINUX/LinuxL02/Task13_03_status_fw.png)

Como vemos, el servicio no está iniciado. Para arrancar el servicio debemos ejecutar lo siguiente.

```bash
$ sudo systemctl start firewalld
```

Ahora volvemos a comprobar si ya está arrancado.

```bash
$ systemctl status firewalld
```

![Estado firewalld](/img/LINUX/LinuxL02/Task13_04_status_fw.png)

Vemos que ya está arrancado, por lo que procedemos con la configuración solicitada. Antes nos cambiamos al usurio root.

```bash
$ sudo su
```

Vamos a ver que puertos tenemos abiertos en la zona pública.

```
# firewall-cmd --zone=public --list-all
```

![Ver configuración zona pública](/img/LINUX/LinuxL02/Task13_05_list_zone_public.png)

Como vemos no hay puertos permitidos. Vamos añadir el puerto 80 como nos han solicitado.

```
# firewall-cmd --permanent --zone=public --add-port=80/tcp
```

![Añadir puerto](/img/LINUX/LinuxL02/Task13_06_add_port.png)

Una vez añadido, recargamos la configuración.

```
# firewall-cmd --reload
```

![Recargar configuración](/img/LINUX/LinuxL02/Task13_07_reload_conf.png)

Si volvemos a comprobar la configuración de la zona pública, vemos que ahora aparece el puerto 80.

```
# firewall-cmd --zone=public --list-all
```

![Ver configuración zona pública](/img/LINUX/LinuxL02/Task13_08_list_zone.png)

Ya no tenemos que hacer más en cuanto al Firewall, puesto que los puertos están cerrados y el 8080 debe permancer así. Aquí no hay bloqueos, sólo permisos para añadir.

Antes de terminar, revisaremos si Apache y Nginx están ejecutandose.

```
# systemctl status httpd

# systemctl status nginx
```

![Estado Apache y Nginx](/img/LINUX/LinuxL02/Task13_09_status_httpd_nginx.png)
