# Docker Nivel 1

## Tarea 5 - Problema con los contenedores Docker

#### Hay un sitio web estático que se ejecuta dentro de un contenedor llamado nautilus, este contenedor se ejecuta en App Server 1. De repente, empezamos a enfrentar algunos problemas con el sitio web estático en App Server 1. Revise el problema para solucionarlo, puede encontrar más detalles a continuación:

#### 1. El volumen /usr/local/apache2/htdocs del contenedor está mapeado con el volumen /var/www/html del host.

#### 2. El sitio web debería ejecutarse en el puerto 8080 del servidor de aplicaciones 1, es decir, el comando curl http://localhost:8080/ debería funcionar en el servidor de aplicaciones 1.

Primero vamos a ver el contenido en /var/www/html

```bash
$ ls -al /var/www/html/
```

![comando ls](/img/DOCKER/DockerL01/Task05_01_ls.png)

Ahora veremos el contenido del fichero index.html

```bash
$ cat /var/www/html/index.html
```

![comando cat](/img/DOCKER/DockerL01/Task05_02_cat.png)

Si hacemos un curl como nos indican, vemos que hay un fallo de conexión y no vemos el contenido del index.html

```bash
$ curl http://localhost:8080/
```

![comando curl](/img/DOCKER/DockerL01/Task05_03_curl.png)

Ese fallo de conexión ya nos da una pista de lo que puede estar sucediendo. Vamos a comprobar si está levantado el contenedor.

```bash
$ docker ps -all
```

![comando docker ps](/img/DOCKER/DockerL01/Task05_04_docker_ps_all.png)

Como vemos el contenedor está caído, por lo que tenemos que levantarlo ejecutando este el siguiente comando.

```bash
$ docker start nautilus
```

![comando docker star](/img/DOCKER/DockerL01/Task05_05_docker_start.png)
