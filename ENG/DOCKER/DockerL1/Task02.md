# Docker Level 1

## Task 2 - Run a Docker Container

#### Nautilus DevOps team is testing some applications deployment on some of the application servers. They need to deploy a nginx container on Application Server 2. Please complete the task as per details given below:

#### 1. On Application Server 2 create a container named nginx_2 using image nginx with alpine tag and make sure container is in running state.

Once we have connected to the server, we are going to see if docker is started.

![systemctl status docker command](/img/DOCKER/DockerL01/Task02_01_systemctl_status_docker.png)

Let's check if our user is in the docker group.

![id command](/img/DOCKER/DockerL01/Task02_02_id.png)

Now we are going to run the container that we are asked for. We use the -d option so that the terminal does not block us.

```bash
$ docker run --name nginx_2 -d nginx:alpine
```

![docker run command](/img/DOCKER/DockerL01/Task02_03_docker_run.png)

To check that the container is up we will run.

```bash
$ docker ps
```

![docker ps command](/img/DOCKER/DockerL01/Task02_04_docker_ps.png)
