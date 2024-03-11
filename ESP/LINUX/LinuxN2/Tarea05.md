# Linux Nivel 2

## Tarea 5 - Autenticación Linux SSH

#### El equipo de administradores de sistemas de xFusionCorp Industries ha configurado algunos scripts en el host jump que se ejecutan a intervalos regulares y realizan operaciones en todos los servidores de aplicaciones en el Centro de Datos Stratos. Para hacer que estos scripts funcionen apropiadamente necesitamos asegurarnos que el usuario thor en el host jump tenga acceso SSH sin contraseña a todos los servidores de aplicaciones a través de sus respectivos usuarios sudo (por ejemplo, tony para el servidor de aplicaciones 1). Basándose en los requisitos, realice lo siguiente:

#### Configure una autenticación sin contraseña desde el usuario thor en el host jump a todos los servidores de aplicaciones a través de sus respectivos usuarios sudo.

Para realizar esta tarea necesitamos generar un par de claves. Una privada y otra pública. La clave privada quedará en el servidor de salto, mientras que la pública la copiaremos a los servidores de aplicaciones.

El comando que utilizaremos para realizar ese paso es ssh-keygen. Este comando es usado para generación, gestión y conversión de claves de autenticación.

Haremos uso de la opción -t para indicar el tipo de clave a usar, en este caso rsa.

```bash
$ ssh-keygen -t rsa
```

![Creación de claves](/img/LINUX/LinuxL02/Task05_01_ssh_keygen.png)

Si listamos el contenido del directorio /home/thor/.ssh vemos que se han generado dos ficheros, `id_rsa` e `id_rsa.pub`

Esos dos ficheros, son las claves privada y pública.

```bash
$ ls -al /home/thor/.ssh
```

![Clave pública y privada](/img/LINUX/LinuxL02/Task05_02_claves.png)

Para copiar la clave pública y poder acceder sin credenciales, usaremos el comando `ssh-copy-id`. Debemos especificar el usuario que usaremos para conectarnos y la IP del servidor. Este comando copiará la clave pública al servidor remoto y la agregará al archivo ~/.ssh/authorized_keys del usuario remoto.

```bash
$ ssh-copy-id tony@172.16.238.10
```

![Copiar claves](/img/LINUX/LinuxL02/Task05_03_ssh_copy_tony.png)

Ahora probaremos el acceso al servidor, con el usuario tony para comprobar que no solicita la contraseña.

![Comprobar acceso](/img/LINUX/LinuxL02/Task05_04_ssh_tony.png)

Ahora vamos a copiar las claves en los otros dos servidores.

![Copiar claves](/img/LINUX/LinuxL02/Task05_05_ssh_copy_steve_banner.png)

Una vez hecho, comprobamos que accedemos sin las credenciales de los usuarios.

![Comprobar accesos](/img/LINUX/LinuxL02/Task05_06_ssh_steve_banner.png)
