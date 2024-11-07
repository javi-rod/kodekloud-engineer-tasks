# Docker Nivel 1

## Tarea 2 - Ejecutar un contenedor Docker

#### El equipo DevOps de Nautilus está probando el despliegue de algunas aplicaciones en algunos de los servidores de aplicaciones. Necesitan desplegar un contenedor nginx en el Servidor de Aplicaciones 2. Por favor, complete la tarea según los detalles que se indican a continuación:

#### 1. En el Servidor de Aplicaciones 2 cree un contenedor llamado nginx_2 usando la imagen nginx con la etiqueta alpine y asegúrese de que el contenedor está en estado de ejecución.

Una vez nos hayamos conectado al servidor, vamos a ver si está docker arrancado.

![comando systemctl status docker](/img/DOCKER/DockerL01/Task02_01_systemctl_status_docker.png)

Vamos a comprobar si nuestro usuario está en el grupo de docker.

![comando id](/img/DOCKER/DockerL01/Task02_02_id.png)

Ahora vamos a correr el contenedor que nos piden. Usamos la opción -d para que no nos bloquee el terminal.

```bash
$ docker run --name nginx_2 -d nginx:alpine
```

![comando docker run](/img/DOCKER/DockerL01/Task02_03_docker_run.png)

Para comprobar que el contenedor está levantado ejecutaremos.

```bash
$ docker ps
```

![comando docker ps](/img/DOCKER/DockerL01/Task02_04_docker_ps.png)
