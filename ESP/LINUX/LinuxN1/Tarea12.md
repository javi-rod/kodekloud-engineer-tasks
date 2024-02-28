# Linux Nivel 1

## Tarea 12 - Copia Remota Linux

#### Uno de los desarrolladores de Nautilus ha copiado datos confidenciales en el host de salto en Stratos DC. Esos datos deben copiarse en uno de los servidores de aplicaciones. Como los desarrolladores no tienen acceso a los servidores de aplicaciones, pidieron al equipo de administradores del sistema que realizara la tarea por ellos.

#### Copie el archivo /tmp/nautilus.txt.gpg del servidor de salto al servidor de aplicaciones 2 en la ubicación /home/nfsshare.

Para hacer la copia desde el servidor de salto hacia uno de los servidores de aplicaciones, tenemos que ejecutar el comando scp como se indica a continuación.

```bash
$ scp /tmp/nautilus.txt.gpg steve@172.16.238.11:/home/nfsshare
```

Ahora si nos conectamos al servidor de destino vía SSH y listamos el contenido del directorio en cuestión, debemos ver el fichero copiado.

![comando scp](/img/LINUX/LinuxL01/Task12_01_scp.png)

![comando ssh](/img/LINUX/LinuxL01/Task12_02_ssh.png)
