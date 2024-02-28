# Linux Nivel 1

## Tarea 7 - Deshabilitar Root Login

#### Después de hacer algunas auditorías de seguridad de los servidores, el equipo de seguridad de xFusionCorp Industries ha implementado algunas nuevas políticas de seguridad. Una de ellas es deshabilitar el root login a través de SSH.

#### Deshabilita el root login a través de SSH en todos los servidores de aplicaciones en el Centro de Datos Stratos.

Los pasos siguientes los haremos en todos los servidores de aplicaciones de la organización

Primero, vamos al directorio /etc/ssh y listamos el contenido

```bash
$ cd /etc/ssh
```

```bash
$ ls -al
```

![comando cd](/img/LINUX/LinuxL01/Task07_01_cd.png)

Como podemos ver, allí está el fichero de configuración de SSH (sshd_config) que editaremos con el comando vi. Si no somos root deberemos ejecutarlo con el comando sudo.

```bash
$ sudo vi sshd_config
```

![comando sudo vi](/img/LINUX/LinuxL01/Task07_02_sudo_vi.png)

Una vez abierto el fichero, iremos a la sección Authentication y cambiaremos el valor de PermitRootLogin de yes a no. Tras editarlo guardamos y cerramos.

![fichero sshd_config](/img/LINUX/LinuxL01/Task07_03_auth.png)

Ahora toca reiniciar el servicio para que coja la nueva configuración.

```bash
$ sudo systemctl restart sshd.service
```

![comando sudo systemctl](/img/LINUX/LinuxL01/Task07_04_sudo_systemctl.png)
