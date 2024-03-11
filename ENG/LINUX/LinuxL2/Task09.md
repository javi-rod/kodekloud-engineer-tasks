# Linux Level 2

## Task 9 - Configure Local Yum repos

#### The Nautilus production support team and security team had a meeting last month in which they decided to use local yum repositories for maintaing packages needed for their servers. For now they have decided to configure a local yum repo on Nautilus Backup Server. This is one of the pending items from last month, so please configure a local yum repository on Nautilus Backup Server as per details given below.

#### a. We have some packages already present at location /packages/downloaded_rpms/ on Nautilus Backup Server.

#### b. Create a yum repo named epel_local and make sure to set Repository ID to epel_local. Configure it to use package's location /packages/downloaded_rpms/.

#### c. Install package wget from this newly created repo.

We will connect via ssh to the Backup server.

![SSH connect](/img/LINUX/LinuxL02/Task09_01_ssh.png)

Now we are going to configure the repository, with the command `createrepo` providing the path to the directory containing the packages. We use sudo as this task requires privileges.

```bash
$ sudo createrepo /packages/downloaded_rpms/
```

![Create repo](/img/LINUX/LinuxL02/Task09_02_createrepo.png)

The Critical error that appears is because a repository already exists in the /packages/downloaded_rpms/ directory.

Once the previous step is done, let's create the configuration file for the 'epel_local' repository in the /etc/yum.repos.d/ directory.

First we will switch to the root user so we don't have to use sudo.

```
$ sudo su
```

And now we run

```
# echo -e "[epel_local]\nname=Epel Local Repo\nbaseurl=file:///packages/downloaded_rpms/\nenabled=1\ngpgcheck=0" > /etc/yum.repos.d/epel_local.repo
```

Here is an explanation of the command:

• echo -e: It is used to print to the console. The -e option allows the use of escape characters.

• "[epel_local]\nname=Epel Local Repo\nbaseurl=file:///packages/downloaded_rpms/\nenabled=1\ngpgcheck=0": This is the string that will be printed. The escape characters are escape characters for new lines, so the output will be printed on multiple lines.

• >: This is a redirection operator. It takes the output of the command to its left and writes it to the file to its right.

• /etc/yum.repos.d/epel_local.repo: This is the file in which the output of the echo command will be written.

In short, with this command you are writing the repository configuration to a new file called epel_local.repo in the /etc/yum.repos.d/ directory. This configuration tells YUM that there is a local repository called epel_local, that it is enabled and that packages can be found in /packages/downloaded_rpms/.

![Config repo](/img/LINUX/LinuxL02/Task09_03_configurar_repo.png)

Finally, we have to install wget, for this we execute the installation command.

```
# yum install wget
```

![Install wget](/img/LINUX/LinuxL02/Task09_04_instalar_wget.png)
