# Linux Level 1

## Task 8 - Linux Archives

#### On Nautilus storage server in Stratos DC, there is a storage location named /data, which is used by different developers to keep their data (non confidential data). One of the developers named mariyam has raised a ticket and asked for a copy of their data present in /data/mariyam directory on storage server. /home is a FTP location on storage server itself where developers can download their data. Below are the instructions shared by the system admin team to accomplish this task.

#### - Make a mariyam.tar.gz compressed archive of /data/mariyam directory and move the archive to /home directory on Storage Server.

Once connected to the server, we will go to the /data directory and list the contents of this and the mariyam directory.

```bash
$ cd /data/
```

```bash
$ ls
```

```bash
$ ls -al mariyam/
```

![cd command](/img/LINUX/LinuxL01/Task08_01_cd.png)

As we can see, in the /mariyam directory there are 3 .txt files. To compress the directory and its contents we will use the following command

```bash
$ tar zcvf mariyam.tar.gz /data/mariyam
```

Command options:

- z : To compress the file using gzip

- c : To create a new archive

- v : To show on screen what is being done

- f : Indicates that the next argument is the file name

![tar command](/img/LINUX/LinuxL01/Task08_02_tar_zcfv.png)

To check that the .tar.gz file has been created, run an ls -al on /data

```bash
$ ls -al
```

![ls command](/img/LINUX/LinuxL01/Task08_03_ls_al.png)

If we want to make sure that the file created contains the .txt files we execute the following command.

```bash
$ tar tvf mariyam.tar.gz
```

The difference between this command and the previous one is the use of the t option, which shows a list of the file contents. This way we verify that all the content has been included.

![tar command](/img/LINUX/LinuxL01/Task08_04_tar_tvf.png)

```bash
$ sudo mv mariyam.tar.gz /home/
```

```bash
$ ls -al /home/
```

![sudo mv command](/img/LINUX/LinuxL01/Task08_05_sudo_mv.png)

As shown in the image above, the file mariyam.tar.gz has been moved.
