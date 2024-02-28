# Linux Nivel 2

## Tarea 4 - Sustitución de cadenas en Linux (sed)

#### Hay algunos datos en Nautilus App Server 2 en Stratos DC. Los datos necesitan ser alterados en varios de los archivos. En Nautilus App Server 2, altere el archivo /home/BSD.txt como se detalla a continuación:

#### a. Elimine todas las líneas que contengan código de palabras y guarde los resultados en el archivo /home/BSD_DELETE.txt. (Tenga en cuenta las mayúsculas y minúsculas)

#### b. Reemplace todas las apariciones de la palabra y (and) a ellas (them) y guarde los resultados en el archivo /home/BSD_REPLACE.txt..

#### Nota: Supongamos que se le pide que sustituya la palabra to por from. En ese caso, asegúrese de no alterar ninguna palabra que contenga la cadena en sí; por ejemplo up**to**, contribu**to**r etc.

Aunque no es necesario para este ejercicio, sí es buena práctica, hacer una copia del fichero a editar. Usaremos sudo ya que en el directorio /home nuestro usario no tiene permiso de escritura.

```bash
$ sudo cp /home/BSD.txt /home/BSD.txt.copy
```

![Copia de seguridad del fichero original](/img/LINUX/LinuxL02/Task04_01_sudo_cp.png)

Para comprobar que se ha hecho la copia del fichero listaremos el directorio /home

```bash
$ ls -al /home/
```

![Listar directorio](/img/LINUX/LinuxL02/Task04_02_ls.png)

Ahora vamos a ver las coincidencias de code en el fichero

```bash
$ cat /home/BSD.txt | grep code
```

![Ver coincidencias palabra code](/img/LINUX/LinuxL02/Task04_03_cat.png)

Para contar el número de veces que aparece ejecutaremos el comando anterior añadiendo una | y el comando wc -l

```bash
$ cat /home/BSD.txt | grep code | wc -l
```

![Contar numero de apariciones de code](/img/LINUX/LinuxL02/Task04_04_cat.png)

Para continuar, vamos a cambiarnos al usuario root.

```bash
$ sudo su
```

![Cambiar a root](/img/LINUX/LinuxL02/Task04_05_sudo_su.png)

A continuación, vamos a eliminar las líneas que contengan la palabra code y crearemos un nuevo fichero con el resultado.

```
# sed '/code/d' /home/BSD.txt > /home/BSD_DELETE.txt
```

`'/code/d'`: Es la expresión que sed va a ejecutar. La barra / se usa para delimitar una expresión regular (en este caso, la palabra ‘code’). La d al final es un comando que le dice a sed que borre las líneas que coincidan con la expresión regular.

![Eliminar lineas que contengan code y crear nuevo fichero](/img/LINUX/LinuxL02/Task04_06_sed.png)

Después vamos a listar el directorio /home para ver que se ha creado el fichero.

```
# ls -al /home/
```

![Listar directorio](/img/LINUX/LinuxL02/Task04_07_ls.png)

Una vez que vemos que se ha creado el fichero, vamos a ver el contenido.

```
# cat /home/BSD_DELETE.txt
```

![Ver contenido fichero](/img/LINUX/LinuxL02/Task04_08_cat.png)

Como vemos ya no hay un punto 1 donde aparecía la palabra code.

Ahora vamos a buscar coincidencias para and. En esta ocasión en lugar de usar un cat y concatenar el grep, como hemos venido haciendo antes, vamos a ejecutar sólo el grep.

```
# grep and /home/BSD.txt
```

![Ver coincidencias and](/img/LINUX/LinuxL02/Task04_09_grep.png)

Tras ver las coincidencias vamos a proceder a remplazar and por them de la forma siguiente.

```
# sed 's/\<and\>/them/g' /home/BSD.txt > /home/BSD_REPLACE.txt
```

`'s/\<and\>/them/g'`: Este es el argumento que le pasamos a sed. s es el comando de sustitución. \<and\> es la palabra que queremos reemplazar (el uso de \< and \> asegura que se trate como una palabra completa y no como parte de otra palabra). them es la palabra con la que queremos reemplazar and. g es una bandera que indica que queremos reemplazar todas las ocurrencias de and en cada línea, no solo la primera.

![Cambiar and por them y crar nuevo fichero](/img/LINUX/LinuxL02/Task04_10_sed.png)

Si vemos el numero de apariciones de and vemos que el resultado es 24

```
# grep and /home/BSD.txt | wc -l
```

![Ver número de coincidencias de and](/img/LINUX/LinuxL02/Task04_11_grep.png)

Vamos a comparar ahora el resultado anterior con el número de apariciones de them en el nuevo fichero.

```
# grep and /home/BSD_REPLACE.txt | wc -l
```

![Ver número de coincidencias de them](/img/LINUX/LinuxL02/Task04_12_grep.png)

Como vemos ambos muestran el mismo número de apariciones, 24.

Para finalizar, vamos a ver las coincidencias de them en el fichero /home/BSD_REPLACE.txt

```
# cat /home/BSD_REPLACE.txt
```

![Ver coincidencias them](/img/LINUX/LinuxL02/Task04_13_grep.png)
