# Linux Nivel 2

## Tarea 8 - Instalar Ansible

#### Durante la reunión semanal, el equipo DevOps de Nautilus discutió sobre las soluciones de automatización y gestión de configuración que querían implementar. Mientras consideraban varias opciones, el equipo ha decidido ir con Ansible por ahora debido a su sencilla configuración y mínimos requisitos previos. El equipo quería empezar a probar el uso de Ansible, por lo que han decidido utilizar el host de salto como un controlador de Ansible para probar diferentes tipos de tareas en el resto de los servidores.

#### Instale la versión 4.9.0 de Ansible en el servidor Jump usando pip3 solamente. Asegúrese de que el binario Ansible está disponible globalmente en este sistema, es decir, todos los usuarios de este sistema son capaces de ejecutar comandos Ansible.

Para hacer este ejercicio podemos usar la siguiente documentación:

https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-and-upgrading-ansible-with-pip

Instalaremos Ansible en su versión 4.9.0 con el comando siguiente

```bash
$ sudo pip3 install ansible==4.9.0
```

![Instalar Ansible](/img/LINUX/LinuxL02/Task08_01_pip3.png)

Una vez instalado, vamos a verificar que funciona, para ellos probamos a ver la versión instalada ejecutando el siguiente comando.

```bash
$ ansible --version
```

![Verifircar versión de Ansible](/img/LINUX/LinuxL02/Task08_02_ansible_version.png)

Ahora vamos comprobar si Ansible está en el PATH. Si nos fijamos en la imagen anterior, veremos que el ejecutable está en /usr/local/bin y ese directorio se encuentra en el PATH.

![Comprobar PATH](/img/LINUX/LinuxL02/Task08_03_path.png)
