# Linux Nivel 2

## Tarea 11 - Linux Configurar sudo

#### Tenemos algunos usuarios en todos los servidores de aplicaciones en Stratos Datacenter. A algunos de ellos se les han asignado nuevos roles y responsabilidades, por lo tanto sus usuarios necesitan ser actualizados con acceso sudo para que puedan realizar tareas de nivel de administrador.

#### a. Proporcione acceso sudo al usuario siva en todos los servidores de aplicaciones.

#### b. Asegúrese de haber configurado sudo sin contraseña para el usuario.

Como en el ejercicio anterior, los pasos siguientes debemos ejecutarlos en cada servidor de apliaciones, previamente nos habremos conectado vía ssh.

Una vez conectado al servidor, nos cambiamos al usuario root por comodidad. Evitamos usar el sudo en cada instrucción.

![Cambiar a usuario root](/img/LINUX/LinuxL02/Task11_01_sudo_su.png)

A continuaciónm, vamos a permitir que siva pueda hacer uso de sudo sin contraseña. Para ello vamos a editar el fichero sudoers de una forma segura con el siguiente comando.

![Editar sudoers](/img/LINUX/LinuxL02/Task11_02_visudo.png)

Una vez abierto el fichero, debemos añadir estas líneas `siva   ALL=(ALL:ALL) NOPASSWD:ALL` tal como se muestra en la imagen.

![Añadir línea](/img/LINUX/LinuxL02/Task11_03_edit_sudo.png)

Una vez añadidas, guardamos y salimos. Y con esto ya tendría permiso.

Otra forma de hacerlo, sería agregando a siva al grupo wheel. Y en el fichero sudoers indicarle `NOPASSWD:ALL` al grupo, como muestro en la siguiente imagen.

![Añadir NOPASSWD:ALL](/img/LINUX/LinuxL02/Task11_04_edit_sudo.png)

Esta segunda forma, es más práctica ya que controlamos por grupo y no usuario. Si tuvieramos muchos usuarios, deberíamos meter una línea por cada uno.
