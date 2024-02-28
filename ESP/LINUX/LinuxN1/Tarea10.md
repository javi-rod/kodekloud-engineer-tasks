# Linux Nivel 1

## Tarea 10 - Linux Access Control List

#### El equipo de seguridad de Nautilus realizó una auditoría en todos los servidores presentes en Stratos DC. Durante la auditoría se identificaron algunos datos/archivos críticos que tenían permisos incorrectos según las normas de seguridad. Una vez que se compartió el informe con el equipo de soporte de producción, empezaron a solucionar los problemas uno por uno. Se ha identificado que uno de los archivos llamado /etc/hosts en el servidor Nautilus App 2 tiene permisos incorrectos, por lo que es necesario corregirlo y establecer las ACL correctas.

#### 1. El usuario propietario y el grupo propietario del archivo deben ser el usuario root.

#### 2. Los demás deben tener permisos de sólo lectura en el archivo.

#### 3. El usuario javed no debe tener ningún permiso sobre el archivo.

#### 4. El usuario eric debe tener permiso de sólo lectura sobre el fichero.

Para ver la ACL del fichero /etc/hosts haremos uso del comando siguiente

```bash
$ getfacl /etc/hosts
```

Como vemos el propietario y grupo son correctos. Otros tiene el permiso de lectura. Por tanto los puntos 1 y 2 están ok.

![comando getfacl](/img/LINUX/LinuxL01/Task10_01_getfacl.png)

Para el punto 3 ejecutaremos el siguiente comando, éste nos permite modificar la ACL en /etc/host. La opción -m es para indicar que vamos a modificar la ACL de un archivo o directorio. La opción -u se usa para indicar que estamos modificando los permisos de un usuario. Después del usuario se indican los permisos que debe tener, en este caso como no debe tener usamos ---

```bash
$ sudo setfacl -m u:javed:--- /etc/hosts
```

![comando sudo setfacl](/img/LINUX/LinuxL01/Task10_02_sudo_setfacl.png)

Para el punto 4, usamos el mismo comando anterior, salvo que en los permisos indicamos r ya que deseamos que pueda leer el fichero.

```bash
$ sudo setfacl -m u:eric:r /etc/hosts
```

![comando sudo setfacl](/img/LINUX/LinuxL01/Task10_03_sudo_setfacl.png)

Si ahora revisamos la ACL, vermos que se han añadido los usuarios con sus respectivos permisos.

```bash
$ getfacl /etc/hosts
```

![comando getfacl](/img/LINUX/LinuxL01/Task10_04_getfacl.png)
