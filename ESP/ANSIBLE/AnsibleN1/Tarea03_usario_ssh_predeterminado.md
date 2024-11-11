# Ansible Nivel 1

## Tarea 3 - Configurar usuario SSH por defecto para Ansible

#### El equipo Nautilus DevOps tiene como objetivo gestionar todos los servidores dentro del stack usando Ansible, utilizando un usuario sudo común en todos los servidores. Planean usar este usuario para varias tareas en cada servidor. Aunque esto no está finalizado, están empezando con las pruebas. Ansible ya está instalado en el host de salto a través de yum. 

#### Aquí está el requisito:

#### En el host de salto, modificar la configuración por defecto de Ansible para permitir el uso de anita como el usuario SSH por defecto para todos los hosts. Asegúrese de hacer los cambios dentro de la configuración por defecto de Ansible sin crear una nueva.

Primero vamos a listar el contenido del directorio /etc/ansible/ para ver los ficheros que tenemos.

![Listar directorio](/img/ANSIBLE/AnsibleL01/Task03_01_ls.png)

Como se aprecia tenemos un fichero de configuración, `ansible.cfg` el cual vamos editar.

Para ello ejecutaremos `sudo vi /etc/ansible/ansible.cfg`

![Editar fichero ansible.cfg](/img/ANSIBLE/AnsibleL01/Task03_02_vi_ansible_conf.png)

Una vez abierto el fichero, sólo debemos añadir lo siguiente:

`remote_user = anita`

![Añadir remote_user](/img/ANSIBLE/AnsibleL01/Task03_03_add_remote_user.png)

Con esto ya tendríamos un usuario por defecto para todos los hosts.