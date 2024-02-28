# Docker Level 1

## Task 5 - Docker Container Issue

#### There is a static website running within a container named nautilus, this container is running on App Server 1. Suddenly, we started facing some issues with the static website on App Server 1. Look into the issue to fix the same, you can find more details below:

#### 1. Container's volume /usr/local/apache2/htdocs is mapped with the host's volume /var/www/html.

#### 2. The website should run on host port 8080 on App Server 1 i.e command curl http://localhost:8080/ should work on App Server 1.

First let's look at the content in /var/www/html

```bash
$ ls -al /var/www/html/
```

![ls command](/img/DOCKER/DockerL01/Task05_01_ls.png)

Now we will see the contents of the file index.html file

```bash
$ cat /var/www/html/index.html
```

![cat command](/img/DOCKER/DockerL01/Task05_02_cat.png)

If we do a curl as indicated, we see that there is a connection failure and we do not see the content of index.html.

```bash
$ curl http://localhost:8080/
```

![curl command](/img/DOCKER/DockerL01/Task05_03_curl.png)

That connection failure already gives us a clue as to what may be happening. Let's check if the container is up.

```bash
$ docker ps -all
```

![docker ps command](/img/DOCKER/DockerL01/Task05_04_docker_ps_all.png)

As we can see the container is down, so we have to raise it by executing the following command.

```bash
$ docker start nautilus
```

![docker star command](/img/DOCKER/DockerL01/Task05_05_docker_start.png)
