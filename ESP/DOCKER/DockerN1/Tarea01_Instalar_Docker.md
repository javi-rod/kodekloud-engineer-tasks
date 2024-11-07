# Docker Nivel 1

## Tarea 1 - Instalar el paquete Docker

#### La semana pasada el equipo DevOps de Nautilus se reunió con el equipo de desarrollo de aplicaciones y decidieron contenerizar varias de sus aplicaciones. El equipo DevOps quiere hacer algunas pruebas según lo siguiente:

#### 1. Instalar los paquetes docker-ce y docker-compose en App Server 1.

#### 2. Inicie el servicio docker.

Para realizar este ejercicio nos basaremos en la documentación oficial https://docs.docker.com/engine/install/centos/

Lo primero, nos conectaremos vía SSH al servidor correspondiente y cambiaremos al usuario root.

![comando SSH](/img/DOCKER/DockerL01/Task01_01_ssh.png)

Una vez conectados, actualizaremos los paquetes.

```
# yum update -y
```

![comando yum update](/img/DOCKER/DockerL01/Task01_02_yum_update.png)

Después de actualizar los paquetes, si hacemos búsqueda por docker, vemos que no aparecen los paquetes necesarios.

```
# yum search docker
```

![comando yum search](/img/DOCKER/DockerL01/Task01_03_yum_search.png)

Vamos a instalar primero yum-utils, que se trata de un conjunto de herramientas de manipulación de repositorios y gestión ampliada de paquetes y contiene la utilidad yum-config-manager que usaremos después.

```
# yum install -y yum-utils
```

![comando yum install](/img/DOCKER/DockerL01/Task01_04_yum_install.png)

Ahora vamos añadir el repositorio de docker para instalar los paquetes requeridos.

```
# yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

![comando yum config manager](/img/DOCKER/DockerL01/Task01_05_yum_config_manager.png)

Una vez hayamos añadido el repositorio, vamos a poder instalar los paquetes necesarios para poder hacer uso de docker.

```
# sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

![comando yum install](/img/DOCKER/DockerL01/Task01_06_yum_install.png)

Debemos verificar que el Fingerprint que nos aperece coincida con el de la documentación.

![fingerprint](/img/DOCKER/DockerL01/Task01_07_fingerprint.png)

Una vez instalado docker, vamos a arrancarlo.

```
# systemctl start docker
```

![comando systemctl start](/img/DOCKER/DockerL01/Task01_08_systemctl_start_docker.png)

Después veremos el estado del servicio, para verificar que arrancó.

```
# systemctl status docker
```

![comando systemctl status docker](/img/DOCKER/DockerL01/Task01_09_systemctl_status_docker.png)

Una vez que vemos que está arrancado, vamos a comprobar que docker compose funciona.

```
# docker compose version
```

![comando docker compose version](/img/DOCKER/DockerL01/Task01_10_docker_compose_version.png)

Y por último, comprobaremos que docker engine está funcionando.

```
# docker run hello-world
```

![comando docker run](/img/DOCKER/DockerL01/Task01_11_docker_run.png)
