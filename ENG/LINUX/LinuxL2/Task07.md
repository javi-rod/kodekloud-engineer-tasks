# Linux Level 2

## Task 7 - Install a package

#### As per new application requirements shared by the Nautilus project development team, serveral new packages need to be installed on all app servers in Stratos Datacenter. Most of them are completed except for git.

#### Therefore, install the git package on all app-servers.

We will have to connect to each of the application servers. In this case I show how to connect to app server 1.

![SSH connect to server](/img/LINUX/LinuxL02/Task07_01_ssh.png)

Once connected, we will update the server packages.

```bash
$ sudo yum update -y
```

![Update packages](/img/LINUX/LinuxL02/Task07_02_yum_update.png)

After upgrading, let's install GIT.

```bash
$ sudo  yum install -y git
```

![Install GIT](/img/LINUX/LinuxL02/Task07_03_yum_install.png)

To verify that it has been installed, we will look at the GIT version.

```bash
$ git version
```

![View GIT version](/img/LINUX/LinuxL02/Task07_04_git_version.png)
