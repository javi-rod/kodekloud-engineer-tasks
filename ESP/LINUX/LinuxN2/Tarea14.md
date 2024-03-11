# Linux Nivel 2

## Tarea 14 - Servidor de correo Postfix Linux

#### xFusionCorp Industries ha planeado configurar un servidor de correo electrónico común en Stork DC. Después de varias reuniones y recomendaciones han decidido utilizar postfix como agente de transferencia de correo y dovecot como servidor IMAP/POP3. Nos gustaría que realizaras los siguientes pasos:

#### 1. Instalar y configurar postfix en el servidor de correo de Stork DC.

#### 2. Cree una cuenta de correo electrónico jim@stratos.xfusioncorp.com identificada por TmPcZjtRQx.

#### 3. Establece su directorio de correo en /home/jim/Maildir.

#### 4. Instala y configura dovecot en el mismo servidor.

Nos conectaremos al servidor de correo por SSH.

![Conexión ssh](/img/LINUX/LinuxL02/Task14_01_ssh.png)

Después nos cambiaremos al usuario root.

```bash
$ sudo su
```

![Cambiar a root](/img/LINUX/LinuxL02/Task14_02_sudo_su.png)

Luego actualizaremos los paquetes instalados.

```
# yum update -y
```

![Actualizar paquetes](/img/LINUX/LinuxL02/Task14_03_yum_update.png)

Cuando haya terminado, instalaremos postfix.

```
# yum install -y postfix
```

![Instalar Postfix](/img/LINUX/LinuxL02/Task14_04_yum_install.png)

Una vez termine la instalación, editaremos el fichero `/etc/postfix/main.cf` que contiene la configuración de Postfix.

Debemos hacer los siguientes cambios.

- Localizar la línea _myhostname_ en el apartado _INTERNET HOST AND DOMAIN NAMES_. Después la descomentamos y modificamos _host.domain.ltd_ por nuestro host y dominio.

- Encontrar la línea _mydomain_, descomentarla, y añadir nuestro dominio.

- En el apartado _SENDING MAIL_ descomentar la línea _myorigin = $mydomain_

- En el apartado _RECEIVING MAIL_ descomentar la línea _inet_interfaces = all_ y comentar la línea _inet_interfaces = localhost_

- Después buscar la línea _mydestination_. Debemos dejar comentada la primera línea y la segunda descomentarla.

- Luego en el apartado _DELIVERY TO MAILBOX_ descomentamos _home_mailbox = Maildir/_

Todos esos cambios se muestran en las siguientes imagenes.

![Editar etc/postfix/main.cf](/img/LINUX/LinuxL02/Task14_05_maincf.png)

![Editar etc/postfix/main.cf](/img/LINUX/LinuxL02/Task14_06_maincf_2.png)

![Editar etc/postfix/main.cf](/img/LINUX/LinuxL02/Task14_07_maincf_3.png)

![Editar etc/postfix/main.cf](/img/LINUX/LinuxL02/Task14_08_maincf_4.png)

Una vez editado, guardamos y salimos.

A continuación, vamos arrancar el servicio de postfix y comprobar que arranca y no hay errores.

```
# systemctl start postfix

# systemctl status postfix
```

![Arrancar postfix](/img/LINUX/LinuxL02/Task14_09_start_status_postfix.png)

Como vemos, le hemos arrancado pero no habilitado, está disabled. Para que arranque cuando se reinicie el servidor, ejecutaremos los comandos siguientes.

```
# systemctl enable postfix

# systemctl status postfix
```

![Habilitar postfix](/img/LINUX/LinuxL02/Task14_10_enable_status_postfix.png)

Ahora vamos a crear el usuario que nos pide la tarea y le asignaremos la password indicada.

![Añadir usuario](/img/LINUX/LinuxL02/Task14_11_add_user.png)

Para probar el funcionamiento de postfix haremos un Telnet al puerto 25. Este puerto es usado por el protocolo SMTP. Si hay conexión, enviaremos un correo al usuario creado anteriormente.

```
# telnet stmail01 25

EHLO localhost
mail from:jim@stratos.xfusioncorp.com
rcpt to:jim@stratos.xfusioncorp.com
DATA
test mail
quit
```

![Telnet](/img/LINUX/LinuxL02/Task14_12_telnet.png)

Como vemos, hemos tenido conexión con nuestro host al puerto 25 y aparentemente hemos podido enviar el correo. Si nos fijamos, aparece queued as 07CD8679B1C6.

El siguiente paso es verificar que se ha enviado el correo, para lo cual cambiaremos de usuario, de root a jim, y ejecutaremos el comando `mailq`. Ese comando nos muestra la cola de correos.

Para hacer el cambio de usuario, usamos el comando `su` seguido del nombre de usuario.

![Cambiar a usuario jim](/img/LINUX/LinuxL02/Task14_13_su.png)

Como vemos no hay ningún correo encolado. Si apareciera un correo, es que algo hemos hecho mal en la configuración del fichero principal. Puede que la IP o el dominio no estén bien puestos.

Vamos a listar el home de jim para ver si se ha creado la carpeta Maildir que configuramos en postfix. Vemos que sí se ha creado la carpeta, eso es buena señal.

![Listar contenido home](/img/LINUX/LinuxL02/Task14_14_ls.png)

Si accedemos al directorio Maildir y listamos el contenido, veremos una carpeta new.

![Listar contenido Maildir](/img/LINUX/LinuxL02/Task14_15_ls.png)

Si listamos el contendio de new, veremos un fichero que es el correo enviado anteriormente. Si hacemos un cat a ese fichero veremos el contenido.

![Listar contenido new](/img/LINUX/LinuxL02/Task14_155_ls.png)

Comprobado el correcto funcionamiento, vamos a instalar el paquete de dovecot, que se trata de un servidor de IMAP y POP3.

```
# yum install -y dovecot
```

![Instalar dovecot](/img/LINUX/LinuxL02/Task14_16_install_dovecot.png)

Después de instalar el paquete, editaremos el fichero `/etc/dovecot/dovecot.conf`. Éste es el archivo de configuración principal de Dovecot.

En este fichero debemos descomentar la línea _protocols = imap pop3 lmtp submission_

![Editar configracion dovecot](/img/LINUX/LinuxL02/Task14_17_dovecotconf.png)

![Editar configracion dovecot](/img/LINUX/LinuxL02/Task14_18_dovecotconf.png)

Luego editaremos el fichero `/etc/dovecot/conf.d/10-mail.conf`. Éste contiene las configuraciones relacionadas con los buzones de correo.

En este fichero tenemos que

- Descomentar la línea _disable_plaitext_auth = yes_. Esta línea indica que Dovecot fallará en la autenticación si el cliente no utiliza SSL o no utiliza autenticación no-plaintext

- En la línea _auth_mechanisms = plain_ añadir login. Esta línea habilita los mecanismos de autenticación PLAIN y LOGIN

![Editar configracion dovecot](/img/LINUX/LinuxL02/Task14_19_mailconf.png)

![Editar configracion dovecot](/img/LINUX/LinuxL02/Task14_20_authconf.png)

![Editar configracion dovecot](/img/LINUX/LinuxL02/Task14_21_authconf.png)

Una vez editado el fichero anterior, modificaremos el fichero `/etc/dovecot/conf.d/10-master.conf`. Éste contiene configuraciones que serán usadas por dovecot.

Aquí debemos buscar _unix_listener auth-userdb_ y descomentar _user_ y _group_ y añadir en ambos postfix.

![Editar configracion dovecot](/img/LINUX/LinuxL02/Task14_22_masterconf.png)

![Editar configracion dovecot](/img/LINUX/LinuxL02/Task14_23_masterconf.png)

Editados los ficheros, arrancaremos el servicio dovecot

```
# systemctl start dovecot

# systemctl status dovecot
```

![Iniciar dovecot](/img/LINUX/LinuxL02/Task14_24_start_dovecot.png)

Lo habilitamos para que incie cuando arranquemos el servidor.

![Habilitar dovecot](/img/LINUX/LinuxL02/Task14_25_enabledovecot.png)

```
# systemctl enable dovecot
```

Para finalizar, haremos una verificación. Lanzaremos un telnet al puerto 110 (usado por el protocolo POP3) para comprobar la conexión.Nos conectaremos con el usuario jim y su contraseña, y veremos el correo enviado anteriormente.

```
# telnet stmail01 110
user jim
pass {given-password}
retr 1
quit
```

![Telnet 110](/img/LINUX/LinuxL02/Task14_26_telnet.png)

Con lo anterior hemos comprobado que la configuración de dovecot es correcta.
