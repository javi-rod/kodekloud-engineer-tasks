# Linux Level 2

## Task 10 - Linux Services

#### As per details shared by the development team, the new application release has some dependencies on the back end. There are some packages/services that need to be installed on all app servers under Stratos Datacenter. As per requirements please perform the following steps:

#### a. Install squid package on all the application servers.

#### b. Once installed, make sure it is enabled to start during boot.

The following steps must be executed on each of the servers, once we have connected via SSH.

First of all, we will switch to the root user, avoiding using sudo for every command.

```bash
$ sudo su
```

![Change to root user](/img/LINUX/LinuxL02/Task10_01_sudo_su.png)

Next we will update the packages already installed.

```
# yum update -y
```

![Update packages](/img/LINUX/LinuxL02/Task10_02_yum_update.png)

Then we will install squid.

```
# yum install squid -y
```

![Install squid](/img/LINUX/LinuxL02/Task10_03_yum_install.png)

Now that we have squid installed, let's see the status of the service.

```
# systemctl status squid
```

![squid service status](/img/LINUX/LinuxL02/Task10_04_yum_status.png)

As we can see it is not started, so we will execute the following commands to start the service and check the status.

```
# systemctl start squid

# systemctl status squid
```

![Start squid service](/img/LINUX/LinuxL02/Task10_05_yum_start.png)

As we can see in the previous image, the service is started, but "disabled". To enable it we will execute the following command.

```
# systemctl enable squid
```

![Enable squid](/img/LINUX/LinuxL02/Task10_06_yum_enable.png)
