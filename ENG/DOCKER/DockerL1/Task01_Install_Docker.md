# Docker Level 1

## Task 1 - Install Docker Package

#### Last week the Nautilus DevOps team met with the application development team and decided to containerize several of their applications. The DevOps team wants to do some testing per the following:

#### 1. Install docker-ce and docker-compose packages on App Server 1.

#### 2. Start docker service.

To perform this exercise we will rely on the official documentation https://docs.docker.com/engine/install/centos/.

First of all, we will connect via SSH to the corresponding server and change to the root user.

![SSH command](/img/DOCKER/DockerL01/Task01_01_ssh.png)

Once connected, we will update the packages.

```
# yum update -y
```

![yum update command](/img/DOCKER/DockerL01/Task01_02_yum_update.png)

After updating the packages, if we search for docker, we see that the necessary packages do not appear.

```
# yum search docker
```

![yum search command](/img/DOCKER/DockerL01/Task01_03_yum_search.png)

Let's first install yum-utils, which is a set of tools for repository manipulation and extended package management and contains the yum-config-manager utility that we will use later.

```
# yum install -y yum-utils
```

![yum install command](/img/DOCKER/DockerL01/Task01_04_yum_install.png)

Now let's add the docker repository to install the required packages.

```
# yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

![yum config manager command](/img/DOCKER/DockerL01/Task01_05_yum_config_manager.png)

Once we have added the repository, we will be able to install the necessary packages to be able to use docker.

```
# sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

![yum install command](/img/DOCKER/DockerL01/Task01_06_yum_install.png)

We must verify that the Fingerprint that appears matches the one in the documentation.

![fingerprint](/img/DOCKER/DockerL01/Task01_07_fingerprint.png)

Once docker is installed, let's start it.

```
# systemctl start docker
```

![systemctl start command](/img/DOCKER/DockerL01/Task01_08_systemctl_start_docker.png)

Then we will see the status of the service, to verify that it has started.

```
# systemctl status docker
```

![systemctl status docker command](/img/DOCKER/DockerL01/Task01_09_systemctl_status_docker.png)

Once we see that it is started, let's check that docker compose is running.

```
# docker compose version
```

![docker compose version command](/img/DOCKER/DockerL01/Task01_10_docker_compose_version.png)

And finally, we will check that docker engine is running

```
# docker run hello-world
```

![docker run command](/img/DOCKER/DockerL01/Task01_11_docker_run.png)
