# Linux Level 1

## Task 2 – Create a group

#### There are specific access levels for users defined by the xFusionCorp Industries system admin team. Rather than providing access levels to every individual user, the team has decided to create groups with required access levels and add users to that groups as needed. See the following requirements:

#### - Create a group named nautilus_sftp_users in all App servers in Stratos Datacenter.

#### - Add the user stark to nautilus_sftp_users group in all App servers. (create the user if doesn't exist).

First of all, we will connect to each of the servers to launch the following commands.

![ssh command](/img/LINUX/LinuxL01/Task02_01_SSH.png)

![ssh command](/img/LINUX/LinuxL01/Task02_02_SSH.png)

![ssh command](/img/LINUX/LinuxL01/Task02_03_SSH.png)

We will use the groupdd command preceded by sudo to create the requested group.

```bash
$ sudo groupadd nautilus_sftp_users
```

As we can see, if we do not launch it with sudo, it will fail.

![groupadd command](/img/LINUX/LinuxL01/Task02_04_groupadd.png)

![sudo groupadd command](/img/LINUX/LinuxL01/Task02_05_sudo_groupadd.png)

To verify that the group has been created, check the /etc/group file for the name of the group in question by executing the following command:

```bash
$ cat /etc/group | grep nautilus_sftp_users
```

![cat command](/img/LINUX/LinuxL01/Task02_06_cat_etc_group.png)

Now, let's see if the user stark exists in the system. To do this we check the /etc/passwd file looking for the user's name.

```bash
$ cat /etc/passwd | grep stark
```

![cat command](/img/LINUX/LinuxL01/Task02_07_cat_etc_passwd.png)

As we can see, the user does not exist, so we add it by executing the useradd command preceded by sudo since it requires privileges.

```bash
$ sudo useradd stark
```

```bash
$  cat /etc/passwd | grep stark
```

After adding the user, if we look for the user in /etc/passwd, we see an entry

![sudo useradd command](/img/LINUX/LinuxL01/Task02_08_sudo_useradd.png)

To add the user to the group, use the usermod command preceded by sudo as shown below.

```bash
$  sudo usermod -a -G nautilus_sftp_users stark
```

Usermod options used:

- -a : To add the user to the group(s).

- -G : To specify the group or groups to add to

To see if the user is actually included in the group, we have two options, one is to run the command groups

```bash
$  groups stark
```

The other is to launch the command id

```bash
$  id stark
```

This is the output of the execution of the above commands.

![sudo usermod command](/img/LINUX/LinuxL01/Task02_09_sudo_usermod.png)

As can be seen in the previous image, the difference between using groups or id is that id provides more information, since we can see the uid, gid, and id of the groups.
