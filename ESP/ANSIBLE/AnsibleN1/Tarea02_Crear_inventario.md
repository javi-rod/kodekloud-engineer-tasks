# Ansible Nivel 1

## Tarea 2 - Crear un inventario de Ansible para probar servidores de aplicaciones


#### El equipo de DevOps de Nautilus está probando los playbooks de Ansible en varios servidores dentro de su stack. Han colocado algunos playbooks en el directorio /home/thor/playbook/ en el host de salto y ahora pretenden probarlas en el servidor de aplicaciones 3 en Stratos DC. Sin embargo, es necesario crear un archivo de inventario para que Ansible se conecte a la aplicación correspondiente. Aquí están los requisitos:

#### a. Crear un archivo de inventario Ansible de tipo ini /home/thor/playbook/inventory en el host de salto.

#### b. Incluya App Server 3 en este inventario junto con las variables necesarias para su correcto funcionamiento.

#### c. Asegúrese de que el nombre de host del inventario se corresponde con el nombre del servidor según la wiki, por ejemplo stapp01 para el servidor de aplicaciones 1 en Stratos DC.

#### _Nota_ : La validación ejecutará el libro de jugadas utilizando el comando ansible-playbook -i inventory playbook.yml. Asegúrese de que el libro de jugadas funciona correctamente sin argumentos adicionales.

Lo primero que vamos hacer es cambiarnos al directorio playbook, listar su contenido y ver el playbook que nos han dejado.

![Cambiar de directorio, listar contenido y ver que tiene el playbook](/img/ANSIBLE/AnsibleL01/Task02_01_cd_ls_cat.png)

A continuación vamos a crear el inventario con el comando vi.

![Crear inventario](/img/ANSIBLE/AnsibleL01/Task02_02_vi_inventory.png)

El inventario contendrá lo siguiente:

`stapp03 ansible_host=172.16.238.12 ansible_user=banner ansible_connection=ssh ansible_password=BigGr33n ansible_ssh_common_args='-o StrictHostKeyChecking=no'`

Con '-o StrictHostKeyChecking=no' evitamos que SSH verifique si la clave del host remoto coincide con la clave conocida para ese host. NO nos preguntará si queremos guardar la nueva clave a la lista de hosts conocidos. Para este ejercicio nos vale, pero en entornos reales está desaconsejado por motivos de seguridad.


![Inventario](/img/ANSIBLE/AnsibleL01/Task02_03_inventory.png)

Ahora que tenemos el inventario creado, vamos ejecutar el playbook tal como indican en el ejercicio `ansible-playbook -i inventory playbook.yml`

![Ejecutar playbook](/img/ANSIBLE/AnsibleL01/Task02_04_play_playbook.png)

Como podemos apreciar, se han realizado dos cambios, que corresponden a nuestras tareas.

Para verificar que lo que hemos hecho está bien, nos conectaremos mediante SSH al servidor de aplicaciones, en este caso el stapp03, y ejecutaremos 

``` bash 
$ sudo systemctl status htppd
```

![Comprobar hhtpd en stapp03](/img/ANSIBLE/AnsibleL01/Task02_05_comprobar_httpd.png)

Como vemos, httpd ha sido instalado y está activo y corriendo.