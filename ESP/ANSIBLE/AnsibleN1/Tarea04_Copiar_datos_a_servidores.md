# Ansible Nivel 1

## Tarea 4 - Copia de datos a servidores de aplicaciones mediante Ansible

#### El equipo DevOps de Nautilus necesita copiar datos desde el host de salto a todos los servidores de aplicaciones en Stratos DC utilizando Ansible. Ejecute la tarea con los siguientes detalles:

#### a. Cree un archivo de inventario /home/thor/ansible/inventory en jump_host y añada todos los servidores de aplicaciones como nodos gestionados.

#### b. Cree un playbook /home/thor/ansible/playbook.yml en el host de salto para copiar el archivo */usr/src/sysops/index.html* en todos los servidores de aplicaciones, colocándolo en */opt/sysops*.

Para empezar nos cambiaremos al directorio de ansible y listaremos el contenido. Como vemos no hay nada, así que procederemos creando el inventario.

![Cambiar de directorio, listar contenido y crear inventario](/img/ANSIBLE/AnsibleL01/Task04_01_cd_ls_vi.png)

Debemos introducir lo siguiente

```
stapp01 ansible_host=172.16.238.10 ansible_connection=ssh ansible_user=tony ansible_ssh_pass=Ir0nM@n
stapp02 ansible_host=172.16.238.11 ansible_connection=ssh ansible_user=steve ansible_ssh_pass=Am3ric@
stapp03 ansible_host=172.16.238.12 ansible_connection=ssh ansible_user=banner ansible_ssh_pass=BigGr33n
```

![Inventario](/img/ANSIBLE/AnsibleL01/Task04_02_inventory.png)

Ahora vamos a crear el playbook, hacemos un `vi playbook.yml` e introducimos lo siguiente:

```yaml
---
- name: Copy file to APP Servers
  hosts: all
  become: yes
  tasks:
    - name: Copy usr/src/sysops/index.html to /opt/sysops on all APP Servers
      copy:
        src: /usr/src/sysops/index.html
        dest: /opt/sysops
```

![Playbook](/img/ANSIBLE/AnsibleL01/Task04_03_playbook.png)

Una vez tengamos el inventario y el playbook, lo ejecutamos con `ansible-playbook -i inventory playbook.yml`

![Ejecutar playbook](/img/ANSIBLE/AnsibleL01/Task04_04_play_playbook.png)

Como vemos se ha producido un cambio en cada servidor, ahora vamos a comprobar que se ha ejecutado correctamente. Para ello nos conectamos vía SSH a cada máquina y listamos el contenido del directorio /opt/sysops

![SSH stapp01 y comprobación](/img/ANSIBLE/AnsibleL01/Task04_05_ssh_stapp01.png)

![SSH stapp02 y comprobación](/img/ANSIBLE/AnsibleL01/Task04_06_ssh_stapp02.png)

![SSH stapp03 y comprobación](/img/ANSIBLE/AnsibleL01/Task04_07_ssh_stapp03.png)

Como vemos en las capturas anteriores, en todos los servidores se ha creado el fichero index.html en el directorio indicado.