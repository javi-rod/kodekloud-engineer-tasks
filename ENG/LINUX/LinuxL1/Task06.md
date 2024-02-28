# Linux Level 1

## Task 6 - Linux User Files

##### There was some users data copied on Nautilus App Server 2 at /home/usersdata location by the Nautilus production support team in Stratos DC. Later they found that they mistakenly mixed up different user data there. Now they want to filter out some user data and copy it to another location. Find the details below:

#### On App Server 2 find all files (not directories) owned by user james inside /home/usersdata directory and copy them all while keeping the folder structure (preserve the directories path) to /media directory.

To search the files in the directory we will use the find command, using -type f to indicate that we want to search for files, as well as using -exec to then execute a command, in this case a cp. We will use --parents to maintain the directory structure. The {} will be replaced by the files and the -- represents the end of the exec command.

```bash
$ find /home/usersdata -type f -user james -exec cp --parents {} /media \;
```

![find command](/img/LINUX/LinuxL01/Task06_01_find.png)

The way to check that all the files have really been copied is the following, we will use the find command with the source path as shown and add an | to run the wc -l command to see the number of files. We launch the same command with the destination path without the user in this case and we should see that both outputs return the same value.

```bash
$ find /home/usersdata -type f -user james| wc -l
```

```bash
$ find /media/home/userdata/ -type f | wc -l
```

![find command](/img/LINUX/LinuxL01/Task06_02_find.png)

As we can see both return the same value, so we have performed the copy well.

In this case we could have executed the following command at first, saving a step.

```bash
$ find /home/usersdata -type f -user ejemplo -exec cp --parents {} /media \; -print | wc -l
```
