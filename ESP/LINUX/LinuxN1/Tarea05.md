# Linux Nivel 1

## Tarea 5 - Expiración del usuario Linux

#### A un desarrollador llamado rose se le ha asignado temporalmente el proyecto Nautilus como recurso de respaldo. Como recurso temporal para este proyecto, necesitamos un usuario temporal para rose. Es una buena idea crear un usuario con una fecha de expiración para que el usuario no pueda acceder a los servidores más allá de ese punto.

#### Por lo tanto, cree un usuario llamado rose en el App Server 3 en Stratos Datacenter. Establezca la fecha de caducidad en 2021-04-15. Asegúrese de que el usuario se crea según el estándar y está en minúsculas.

![Comando ssh](/img/LINUX/LinuxL01/Task05_01_ssh.png)

Una vez conectados al servidor, haremos uso del comando useradd precedido de sudo, requiere privilegios, y usaremos la opción -e para indicar que queremos que expire la cuenta en una fecha dada.

```bash
$ sudo useradd -e 2021-04-15 rose
```

![Comando ssh](/img/LINUX/LinuxL01/Task05_02_sudo_useradd.png)

Ahora vamos a verificar que la cuenta se ha configurado para expirar en la fecha indicada. Para ello usaremos el comando chage. Este comando se usa para modificar datos de expiración de la contraseña de un usuario. Usaremos la opción -l para la listar la información de la contraseña del usuario.

```bash
$ sudo chage -l rose
```

![Comando ssh](/img/LINUX/LinuxL01/Task05_03_sudo_chage.png)

Como vemos en el apartado "Account expieres" la fecha coincide con el valor dado anteriormente.
