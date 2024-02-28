# Linux Level 1

## Task 3 - Create a Linux User with non-interactive shell

#### The System admin team of xFusionCorp Industries has installed a backup agent tool on all app servers. As per the tool's requirements they need to create a user with a non-interactive shell.

#### Therefore, create a user named anita with a non-interactive shell on the App Server 1.

Once we have connected to the required server, we will launch the useradd command seen earlier in task01 with the -s option to indicate the path to the user's login shell.

```bash
$ sudo useradd anita -s /sbin/nologin
```

![sudo useradd command](/img/LINUX/LinuxL01/Task03_01_sudo_useradd.png)

To check that everything went well, we will check if in /etc/passwd the user has as shell the value indicated above.

```bash
$ cat /etc/passwd | grep anita
```

![cat command](/img/LINUX/LinuxL01/Task03_02_cat_etc_passwd.png)
