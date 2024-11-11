# Ansible Nivel 1

## Tarea 5 - Creación de archivos en servidores de aplicaciones mediante Ansible

#### El equipo DevOps de Nautilus está probando varios módulos de Ansible en servidores de Stratos DC. Actualmente se están centrando en la creación de archivos en hosts remotos utilizando Ansible. Aquí están los detalles:

#### a. Crear un archivo de inventario ~/playbook/inventory en el host de salto e incluir todos los servidores de aplicaciones.

#### b. Crear un playbook ~/playbook/playbook.yml para crear un archivo en blanco /tmp/opt.txt en todos los servidores de aplicaciones.

#### c. Establezca los permisos del archivo /tmp/opt.txt en 0777.

#### d. Asegúrese de que el usuario/grupo propietario del archivo /tmp/opt.txt es tony en el servidor de aplicaciones 1, steve en el servidor de aplicaciones 2 y banner en el servidor de aplicaciones 3.

#### _Nota_: La validación ejecutará el playbook mediante el comando ansible-playbook -i inventory playbook.yml, por lo que debe asegurarse de que el playbook funcione correctamente sin argumentos adicionales.

Lo primero que vamos hacer es cambiarnos al directorio playbook y crear el inventario.

![Cambiar de directorio, listar contenido y crear inventario](/img/ANSIBLE/AnsibleL01/Task05_01_cd_vi.png)

El inventario debe contener lo siguiente

```
stapp01 ansible_host=172.16.238.10 ansible_connection=ssh ansible_user=tony ansible_ssh_pass=Ir0nM@n
stapp02 ansible_host=172.16.238.11 ansible_connection=ssh ansible_user=steve ansible_ssh_pass=Am3ric@
stapp03 ansible_host=172.16.238.12 ansible_connection=ssh ansible_user=banner ansible_ssh_pass=BigGr33n
```

![Contenido inventario](/img/ANSIBLE/AnsibleL01/Task05_02_inventory.png)

Ahora que tenemos el inventario, vamos a crear el playbook


![Crear playbook](/img/ANSIBLE/AnsibleL01/Task05_03_vi_playbook.png)

El playbook tendrá este aspecto

```yaml
---
- name: Create empty file to APP Servers
  hosts: all
  become: yes
  tasks:
    - name: Create file /tmp/opt.txt on all servers with 0777 permissions
      file:
         path: /tmp/opt.txt
         state: touch
         mode: '0777'

    - name: Set owner and group for each server
      file:
        path: /tmp/opt.txt
        owner: "{{ item.owner }}"
        group: "{{ item.group }}"
      with_items:
       - { name: "stapp01", owner: "tony", group: "tony" }
       - { name: "stapp02", owner: "steve", group: "steve" }
       - { name: "stapp03", owner: "banner", group: "banner" }
      when: inventory_hostname == item.name
```

![Contenido del playbook](/img/ANSIBLE/AnsibleL01/Task05_04_playbook.png)

Ahora que tenemos creados tanto el inventario como el playbook, vamos a ejecutarlo.

![Ejecución del playbook](/img/ANSIBLE/AnsibleL01/Task05_05_play_playbook.png)

Como vemos en la salida de la ejecución, en cada servidor se han realizado dos cambios, que corresponden a nuestras dos tareas.

Ahora nos vamos a conectar a cada servidor de aplicaciones, y vamos a comprobar que se ha creado en /tmp/ el fichero opt.txt con propietario y grupo tal como indican en el enunciado, así como el permiso 0777

![Conexion SSH a stapp01 y comprobación](/img/ANSIBLE/AnsibleL01/Task05_06_ssh_ls_stapp01.png)

![Conexion SSH a stapp02 y comprobación](/img/ANSIBLE/AnsibleL01/Task05_07_ssh_ls_stapp02.png)

![Conexion SSH a stapp03 y comprobación](/img/ANSIBLE/AnsibleL01/Task05_08_ssh_ls_stapp03.png)