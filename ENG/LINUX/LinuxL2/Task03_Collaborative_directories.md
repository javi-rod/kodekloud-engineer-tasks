# Linux Level 2

## Task 3 - Linux Collaborative Directories

#### The Nautilus team doesn't want its data to be accessed by any of the other groups/teams due to security reasons and want their data to be strictly accessed by the devops group of the team.

#### Setup a collaborative directory /devops/data on app server 3 in Stratos Datacenter.

#### The directory should be group owned by the group devops and the group should own the files inside the directory. The directory should be read/write/execute to the user and group owners, and others should not have any access.

Once connected to the server we are going to create the /devops/data directory using the -p option to create the /devops/data structure.

```bash
$ sudo mkdir -p /devops/data
```

![Create directory and subdirectory](/img/LINUX/LinuxL02/Task03_01_sudo_mkdir.png)

If we list the contents of /devops/ we will see that it has been created (represented by the .) and the subdirectory data.

```bash
$ ls -al /devops/
```

![List directory](/img/LINUX/LinuxL02/Task03_02_ls.png)

To change the directory group and subdirectory we will execute the following command

```bash
$ sudo chown -R :devops /devops
```

![Change group in directory and subdirectory](/img/LINUX/LinuxL02/Task03_03_sudo_chown.png)

We use the -R option to make it recursive. The change will be applied to /devops and everything below it.

If we list the contents of /devops/ again we see that the group has changed for devops and for data.

![List directory](/img/LINUX/LinuxL02/Task03_04_ls.png)

Finally, to give the permissions we will use the command chmod with sudo.

```bash
sudo chmod 770 /devops/data
```

![Change permissions](/img/LINUX/LinuxL02/Task03_05_sudo_chmod.png)

The 770 represents full permissions (read, write and execute) for owner and group and no permissions for others.

If we run an ls with sudo on /devops we will see the new permissions. We must use sudo because banner does not have permissions on that directory, not being a popietary nor a member of the devops group.

```bash
$ sudo ls -al /devops/
```

![List directory](/img/LINUX/LinuxL02/Task03_06_sudo-ls.png)
