# Linux Nivel 2

## Tarea 2 - Banner en Linux

#### Durante la reunión mensual de cumplimiento, se señaló que varios servidores en el Stratos DC no tienen un banner válido. El equipo de seguridad ha proporcionado varias plantillas aprobadas que deben aplicarse a los servidores para mantener el cumplimiento. Estas plantillas se mostrarán al usuario cuando inicie sesión correctamente.

#### Actualice el mensaje del día en todos los servidores de aplicaciones y bases de datos para Nautilus. Utilice la plantilla aprobada que se encuentra en /home/thor/nautilus_banner en el servidor de salto.

Lo primero que vamos hacer es visualizar el contenido del banner.

```bash
cat /home/thor/nautilus_banner
```

![Visualizar contenido de la plantilla del banner](/img/LINUX/LinuxL02/Task02_01_banner_template.png)

Después abrimos otro terminal y nos conectamos a uno de los servidores y editaremos el fichero /etc/motd. Ese fichero es el que debemos editar para incluir un mensaje o banner una vez iniciada la sesión.

Una vez conectado al servidor visualizaremos si tiene algún banner.

```bash
$ cat /etc/motd
```

![Ver si motd tiene algun contendio](/img/LINUX/LinuxL02/Task02_02_cat_etc_motd.png)

Como vemos no tiene ninguno.

Editamos el fichero con sudo ya que requiere privilegios

```bash
$ sudo vi /etc/motd
```

![Editar fichero motd](/img/LINUX/LinuxL02/Task02_03_vi_etc_motd.png)

Copiamos el contenido del banner del equipo de salto al fichero y guardamos y salimos.

![Añadir banner en el fichero motd](/img/LINUX/LinuxL02/Task02_04_banner.png)

Para verificar que se guardó correctamente visualizamos de nuevo el contenido del fichero /etc/motd.

```bash
$ cat /etc/motd
```

Estos pasos hay que realizarlos en cada servidor.
