# Docker Nivel 1

## Tarea 3 - Eliminar contenedor Docker

#### Uno de los desarrolladores del proyecto Nautilus creó un contenedor en App Server 2. Este contenedor fue creado sólo para pruebas y ahora necesitamos eliminarlo. Realice esta tarea según los detalles que se indican a continuación:

#### Elimine un contenedor llamado kke-container, que se ejecuta en App Server 2 en Stratos DC.

Vamos a verificar que está corriendo el contenedor

```bash
$ docker ps
```

![comando docker ps](/img/DOCKER/DockerL01/Task03_01_docker_ps.png)

Para eliminar el contenedor ejecutaremos el siguiente comando. Usamos la opción -f para forzar la eliminación. Después comprobaremos que el contenedor ha sido eliminado.

```bash
$ docker rm -f kke-container
```

```bash
$ docker ps
```

![comando docker rm](/img/DOCKER/DockerL01/Task03_02_docker_rm.png)
