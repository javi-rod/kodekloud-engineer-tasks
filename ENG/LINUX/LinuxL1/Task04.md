# Linux Level 1

## Task 4 - Linux User Without Home

#### The system admins team of xFusionCorp Industries has set up a new tool on all app servers, as they have a requirement to create a service user account that will be used by that tool.

#### Create a user named ammar in App Server 2 without a home directory.

Via SSH we connect to the server in question

![ssh command](/img/LINUX/LinuxL01/Task04_01_ssh.png)

Once connected, we will execute the useradd command, already seen in previous tasks, with the -M option to indicate that the user will not have a home directory.

```bash
$ sudo useradd -M ammar
```

![sudo useradd command](/img/LINUX/LinuxL01/Task04_02_sudo_useradd.png)

To verify that the user has been created, check the /etc/passwd file for the user.

```bash
$ cat /etc/passwd | grep ammar
```

As we can see in the file, the user has been created, but the home is displayed.

![cat command](/img/LINUX/LinuxL01/Task04_03_cat_etc_passwd.png)

Not to worry, if we make a list of the /home directory we will see that no home directory has been created for the user in question.

```bash
$ ls -al /home/
```

![ls command](/img/LINUX/LinuxL01/Task04_04_ls_al.png)
