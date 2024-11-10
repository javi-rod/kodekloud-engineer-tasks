# Ansible Nivel 1

## Tarea 1 - Solucionar problemas y crear Ansible Playbook


#### Un playbook de Ansible necesita completarse en el host de salto, donde un miembro del equipo lo dejó. A continuación se presentan los detalles:


#### - El archivo de inventario /home/thor/ansible/inventory requiere ajustes. El playbook debe ejecutarse en App Server 3 en Stratos DC. Actualice el inventario en consecuencia.


#### - Crear un playbook /home/thor/ansible/playbook.yml. Incluir una tarea para crear un archivo vacío /tmp/file.txt en App Server 3.


#### _Nota_ : La validación ejecutará el playbook mediante el comando ansible-playbook -i inventory playbook.yml. Asegúrese de que el playbook funciona sin argumentos adicionales.

Lo primero vamos a cambiar al directorio de ansible y listar el contenido. Después hacemos un cat al inventario para ver su contenido y que debemos cambiar.

![Cambiar de directorio, listar contenido y ver que tiene el inventario](/img/ANSIBLE/AnsibleL01/Task01_01_cd_ansible_cat_inventory.png)

Como podemos ver, el inventario contiene los datos de otro servidor, debemos modificarlo para conectarnos al App Server 3. Para editar el fichero ejecutaremos:

```bash
$ vi intentory
```
Ahora debemos cambiar los datos del fichero por los datos siguientes:

```stapp03 ansible_host=172.16.238.12 ansible_user=banner ansible_password=BigGr33n ansible_ssh_common_args='-o StrictHostKeyChecking=no' ```

ansible_ssh_common_args='-o StrictHostKeyChecking=no' sirve para que SSH no verifique si la clave del host remoto coincide con la clave conocida para ese host. Se usa en este ejercicio por sencillez, para que NO pregunte si queremos agregar la nueva clave a la lista de hosts conocidos. En entornos reales se desaconseja por motivos de seguridad.

![Editar inventario](/img/ANSIBLE/AnsibleL01/Task01_02_vi_inventory.png)

Una vez editado, vamos crear el playbook.

```bash
$ vi playbook.yml
```

![Crear playbook](/img/ANSIBLE/AnsibleL01/Task01_03_vi_playbook.png)

Después introduciremos lo siguiente

```yaml
---
- name: Create empty file in /tmp/file.txt
  hosts: stapp03
  become: yes

  tasks:
    - name: Execute Create empty file in /tmp/file.txt
      ansible.builtin.file:
        path: /tmp/file.txt
        state: touch
```

![Playbook](/img/ANSIBLE/AnsibleL01/Task01_04_playbook.png)

Ya tenemos el playbook creado, lo vamos a ejecutar tal como indican en el enunciado.

```bash
$ ansible-playbook -i inventory playbook.yml
```

![Ejecutar paybook](/img/ANSIBLE/AnsibleL01/Task01_05_play_playbook.png)

Como podemos ver, hubo un cambio en stapp03. Vamos a comprobar si realmente se ha realizado la tarea. Recordemos, debe crearse un fichero /tmp/file.txt.

Para realizar la comprobación, nos conectamos ssh al servidor, en este caso es stapp03, y luego hacemos un listar al directorio /tmp/

![ssh app03](/img/ANSIBLE/AnsibleL01/Task01_06_ssh_app3.png)

Como podemos ver, se ha creado el fichero en el directorio indicado.