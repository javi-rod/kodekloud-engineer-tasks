# Linux Level 1

## Task 9 - Linux File Permissions

#### There are new requirements to automate a backup process that was performed manually by the xFusionCorp Industries system admins team earlier. To automate this task, the team has developed a new bash script xfusioncorp.sh. They have already copied the script on all required servers, however they did not make it executable on one the app server i.e App Server 2 in Stratos Datacenter.

#### Please give executable permissions to /tmp/xfusioncorp.sh script on App Server 2. Also make sure every user can execute it.

If we do an ls -al on the file we can see that it does not have any permissions.

```bash
$ ls -al /tmp/xfusioncorp.sh
```

![ls command](/img/LINUX/LinuxL01/Task09_01_ls_al.png)

To give the requested permissions, we will use the command chmod followed by 755 and the file in question.

We use 755 to give the following permissions:

- To the owner, we give read (r), write (w) and execute (x) permissions, hence the 7.

- To the group, we give read (r) and execute (x) permissions, hence the 5

- To others, we give permission to
  read (r) and execute (x), hence the 5

These numbers are for using the following binary notation:

r (4) w (2) x (1) - 7 is full permission.

r (4) w (2) - 6 permission read - write

r(4) x(1) - permission read and execute

If I remember correctly, the normal thing is to give permission of read and execution and not only the one of execution since if not others could not execute the .sh hence to use the notation 5 instead of 1.

```bash
$ sudo chmod 755 /tmp/xfusioncorp.sh
```

To check it, we list the file

```bash
$ ls -al /tmp/xfusioncorp.sh
```

![sudo chmod command](/img/LINUX/LinuxL01/Task09_02_sudo_chmod.png)
