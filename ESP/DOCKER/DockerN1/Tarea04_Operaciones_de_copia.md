# Docker Nivel 1

## Tarea 4 - Operaciones de copia en Docker

#### El equipo Nautilus DevOps tiene algunos datos confidenciales presentes en App Server 3 en Stratos Datacenter. Hay un contenedor ubuntu_latest ejecutándose en el mismo servidor. Recibimos una solicitud para copiar algunos de los datos desde el host docker al contenedor. A continuación se presentan más detalles acerca de la tarea:

#### En App Server 3 en Stratos Datacenter copiar un archivo encriptado /tmp/nautilus.txt.gpg desde el host docker al contenedor ubuntu_latest (ejecutándose en el mismo servidor) en la ubicación /home/. Por favor, no intente modificar este archivo de ninguna manera.

Ejecutaremos un `docker ps` para ver los contenedores que están corriendo.

![comando docker ps](/img/DOCKER/DockerL01/Task04_01_docker_ps.png)

Si listamos el contenido del directorio /tmp/ vemos el fichero nautilus.txt.gpg que nos indican en el ejercicio.

![comando ls](/img/DOCKER/DockerL01/Task04_02_ls.png)

Para copiar el contenido del host al /home/ del contenedor, debemos ejecutar el comando siguiente.

```bash
$ docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/home/
```

![comando docker cp](/img/DOCKER/DockerL01/Task04_03_docker_cp.png)

Para verificar que se ha copiado el fichero, vamos a lanzar el siguiente comando.

```bash
$ docker exec buntu_latest ls -al /home/
```

![comando docker exec](/img/DOCKER/DockerL01/Task04_04_docker_exec.png)
