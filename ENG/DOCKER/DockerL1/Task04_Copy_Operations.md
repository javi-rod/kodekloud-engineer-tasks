# Docker Level 1

## Task 4 - Docker Copy Operations

#### The Nautilus DevOps team has some confidential data present on App Server 3 in Stratos Datacenter. There is a container ubuntu_latest running on the same server. We received a request to copy some of the data from the docker host to the container. Below are more details about the task:

#### On App Server 3 in Stratos Datacenter copy an encrypted file /tmp/nautilus.txt.gpg from docker host to ubuntu_latest container (running on same server) in /home/ location. Please do not try to modify this file in any way.

We will run a `docker ps` to see which containers are running.

![docker ps command](/img/DOCKER/DockerL01/Task04_01_docker_ps.png)

If we list the contents of the /tmp/ directory we see the file nautilus.txt.gpg indicated in the exercise.

![ls command](/img/DOCKER/DockerL01/Task04_02_ls.png)

To copy the contents of the host to the container's /home/, we must execute the following command.

```bash
$ docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/home/
```

![docker cp command](/img/DOCKER/DockerL01/Task04_03_docker_cp.png)

To verify that the file has been copied, we will launch the following command.

```bash
$ docker exec buntu_latest ls -al /home/
```

![docker exec command](/img/DOCKER/DockerL01/Task04_04_docker_exec.png)
