# Linux Level 1

## Task 1 – Create a user

#### For security reasons the xFusionCorp Industries security team has decided to use custom Apache users for each web application hosted, rather than its default user. This will be the Apache user, so it shouldn't use the default home directory. Create the user as per requirements given below:

#### - Create a user named john on the App server 3 in Stratos Datacenter.

#### - Set its UID to 1606 and home directory to /var/www/john.

The first thing we are going to do is to connect via SSH with the following command (REMEMBER: the user and host may vary)

```bash
$ ssh banner@172.16.238.12
```

![ssh command](/img/LINUX/LinuxL01/Task01_01_SSH.png)

Once connected to the server, we will execute the following command

```bash
$ sudo useradd john -d /var/www/john -u 1606
```

Useradd options used:

- -d : To indicate the path to the home directory.

- -u : To set the UID

The above command must be launched with sudo as it requires privileges, otherwise it will fail as shown below.

![useradd command](/img/LINUX/LinuxL01/Task01_02_useradd.png)

![sudo useradd command](/img/LINUX/LinuxL01/Task01_03_sudo_useradd.png)

To check that the user has been created with the correct options, we will take a look at the /etc/passwd file

```bash
$ cat /etc/passwd
```

As we can see, the user has been created with the requested UID and directory

![cat command](/img/LINUX/LinuxL01/Task01_04_cat_etc_passwd.png)
