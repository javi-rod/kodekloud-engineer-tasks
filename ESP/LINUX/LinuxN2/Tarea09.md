# Linux Nivel 2

## Tarea 9 - Configurar repositorios Yum locales

#### El equipo de soporte de producción y el equipo de seguridad de Nautilus tuvieron una reunión el mes pasado en la que decidieron utilizar repositorios yum locales para mantener los paquetes necesarios para sus servidores. Por ahora han decidido configurar un repositorio yum local en Nautilus Backup Server. Este es uno de los puntos pendientes del mes pasado, así que por favor configure un repositorio yum local en el Servidor de Respaldo Nautilus como se detalla a continuación.

#### a. Tenemos algunos paquetes ya presentes en la ubicación /packages/downloaded_rpms/ en Nautilus Backup Server.

#### b. Cree un repositorio yum llamado epel_local y asegúrese de establecer el ID de repositorio como epel_local. Configúrelo para utilizar la ubicación del paquete /packages/downloaded_rpms/.

#### c. Instale el paquete wget desde este repositorio recién creado.

Nos conectaremos por ssh al servidor de Backup.

![Conectarse vía SSH](/img/LINUX/LinuxL02/Task09_01_ssh.png)

Ahora vamos a configurar el repositorio, con el comando `createrepo` facilitando la ruta del directorio que contiene los paquetes. Usamos sudo ya que esta tarea requiere privilegios.

```bash
$ sudo createrepo /packages/downloaded_rpms/
```

![Crear repo](/img/LINUX/LinuxL02/Task09_02_createrepo.png)

El error Critical que aparece es porque ya existe un repositorio en el directorio /packages/downloaded_rpms/

Una vez realizado el paso anterior, vamos a crear el archivo de configuración para el repositorio 'epel_local' en el directorio /etc/yum.repos.d/

Antes cambiaremos al usuario root para no tener que usar el sudo.

```
$ sudo su
```

Y ahora ejecutaremos

```
# echo -e "[epel_local]\nname=Epel Local Repo\nbaseurl=file:///packages/downloaded_rpms/\nenabled=1\ngpgcheck=0" > /etc/yum.repos.d/epel_local.repo
```

Aquí una explicación del comando:

• echo -e: Se utiliza para imprimir en la consola. La opción -e permite el uso de caracteres de escape.

• "[epel_local]\nname=Epel Local Repo\nbaseurl=file:///packages/downloaded_rpms/\nenabled=1\ngpgcheck=0": Esta es la cadena que se imprimirá. Los \n son caracteres de escape para nuevas líneas, por lo que la salida se imprimirá en varias líneas.

• >: Este es un operador de redirección. Toma la salida del comando a su izquierda y la escribe en el archivo a su derecha.

• /etc/yum.repos.d/epel_local.repo: Este es el archivo en el que se escribirá la salida del comando echo.

Resumiendo, con este comando está escribiendo la configuración del repositorio en un nuevo archivo llamado epel_local.repo en el directorio /etc/yum.repos.d/. Esta configuración le dice a YUM que hay un repositorio local llamado epel_local, que está habilitado y que los paquetes se pueden encontrar en /packages/downloaded_rpms/.

![Configurar repo](/img/LINUX/LinuxL02/Task09_03_configurar_repo.png)

Por último, nos queda instalar wget, para ello ejecutamos el comando de instalación.

```
# yum install wget
```

![Instalar wget](/img/LINUX/LinuxL02/Task09_04_instalar_wget.png)
