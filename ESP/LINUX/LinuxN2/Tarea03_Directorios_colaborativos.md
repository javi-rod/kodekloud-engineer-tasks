# Linux Nivel 2

## Tarea 3 - Directorios colaborativos en Linux

#### El equipo Nautilus no quiere que sus datos sean accedidos por ninguno de los otros grupos/equipos debido a razones de seguridad y quieren que sus datos sean estrictamente accedidos por el grupo devops del equipo.

#### Configura un directorio colaborativo /devops/data en el servidor de aplicaciones 3 en el centro de datos Stratos.

#### El directorio debe ser propiedad del grupo devops y el grupo debe ser dueño de los archivos dentro del directorio. El directorio debe ser de lectura/escritura/ejecución para el usuario y los propietarios del grupo, y los demás no deben tener ningún acceso.

Una vez conectados al servidor vamos a crear el directorio /devops/data haciendo uso de la opción -p para que se cree la estructura /devops/data

```bash
$ sudo mkdir -p /devops/data
```

![Crear directorio y subdirectorio](/img/LINUX/LinuxL02/Task03_01_sudo_mkdir.png)

Si listamos el contenido de /devops/ veremos que se ha creado éste (representado por el .) y el subdirectorio data.

```bash
$ ls -al /devops/
```

![Listar directorio](/img/LINUX/LinuxL02/Task03_02_ls.png)

Para cambiar el grupo de del directorio y el subdirectorio ejecutaremos el siguiente comando.

```bash
$ sudo chown -R :devops /devops
```

![Cambiar grupo de forma recursiva](/img/LINUX/LinuxL02/Task03_03_sudo_chown.png)

Usamos la opción -R para que sea recursivo. Se aplicará el cambio a /devops y todo lo que haya por debajo de él.

Si volvemos a listar el contenido de /devops/ vemos que el grupo ha cambiado para devops y para data.

![Listat directorio](/img/LINUX/LinuxL02/Task03_04_ls.png)

Por último, para dar los permisos usaremos el comando chmod precedido de sudo.

```bash
$ sudo chmod 770 /devops/data
```

![Cambiar permisos](/img/LINUX/LinuxL02/Task03_05_sudo_chmod.png)

El 770 representa permisos totales (lectura, escritura y ejecución) para propietario y grupo y sin permisos para otros.

Si ejecutamos un ls con sudo sobre /devops veremos los nuevos permisos. Debemos usar sudo porque banner no tiene permisos sobre ese directorio, al no ser propietario ni miembro del grupo devops.

```bash
$ sudo ls -al /devops/
```

![Listar directorio](/img/LINUX/LinuxL02/Task03_06_sudo-ls.png)
