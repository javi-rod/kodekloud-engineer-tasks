# Docker Level 1

## Task 3 - Docker Delete Container

#### One of the Nautilus project developers created a container on App Server 2. This container was created for testing only and now we need to delete it. Accomplish this task as per details given below:

#### Delete a container named kke-container, its running on App Server 2 in Stratos DC.

Let's check that the container is running

```bash
$ docker ps
```

![docker ps command](/img/DOCKER/DockerL01/Task03_01_docker_ps.png)

To delete the container we will execute the following command. We use the -f option to force the deletion. Then we will check that the container has been deleted.

```bash
$ docker rm -f kke-container
```

```bash
$ docker ps
```

![docker rm command](/img/DOCKER/DockerL01/Task03_02_docker_rm.png)
