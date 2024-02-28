# Linux Level 2

## Task 1 - Create a Cron Job

#### The Nautilus system admins team has prepared scripts to automate several day-to-day tasks. They want them to be deployed on all app servers in Stratos DC on a set schedule. Before that they need to test similar functionality with a sample cron job. Therefore, perform the steps below:

#### a. Install cronie package on all Nautilus app servers and start crond service.

#### b. Add a cron \*/5 \* \* \* \* echo hello > /tmp/cron_text for root user.

We will connect to the 3 application servers with the command ssh user@ip as shown in the following screenshots.

![SSH connection Nautilus App 1](/img/LINUX/LinuxL02/Task01_01_ssh.png)

![SSH connection Nautilus App 2](/img/LINUX/LinuxL02/Task01_02_ssh.png)

![SSH connection Nautilus App 3](/img/LINUX/LinuxL02/Task01_03_ssh.png)

Once connected to each of the servers, we will launch the following commands.

First, we are going to install the cronie package as shown below.

```bash
$ sudo yum install cronie
```

![Install cronie package](/img/LINUX/LinuxL02/Task01_04_sudo_yum_install_cronie.png)

Once installed, we will start the service

```bash
$ sudo systemctl start crond
```

![Start crond service](/img/LINUX/LinuxL02/Task01_05_sudo_systemctl_start_crond.png)

As we can see we get a Warning. We have to execute the command indicated, to reload the configuration of the systemd manager. Among other things the command reloads all the unit files, which is precisely what warns us that it has changed.

```bash
$ sudo systemctl daemon-reload
```

![Reload config](/img/LINUX/LinuxL02/Task01_06_sudo_systemctl_daemon_reload.png)

To see that the service is up we launch the following command

```bash
$ sudo systemctl status crond
```

![crond service status](/img/LINUX/LinuxL02/Task01_07_sudo_systemctl_status_crond.png)

Once we have verified that it is started we are going to edit the file /etc/crontab. Previously we will change to the root user.

```bash
$ sudo su
```

![Change to root](/img/LINUX/LinuxL02/Task01_08_sudo_su.png)

```
# vi /etc/crontab
```

![Edit crontab](/img/LINUX/LinuxL02/Task01_09_vi_etc_crontab.png)

Add the line indicated in paragraph b and exit and save.

![Add job](/img/LINUX/LinuxL02/Task01_10_edit_crontab.png)

If we now check the contents of /etc/crontab we will see the added line

![View crontab](/img/LINUX/LinuxL02/Task01_11_cat_crontab.png)

Another way to edit the crontab would be to execute the following command.

```
# crontab -e
```

![Edit crontab](/img/LINUX/LinuxL02/Task01_12_crontab_e.png)

We add the indicated line and save and close.

![Add job](/img/LINUX/LinuxL02/Task01_13_edit_crontab.png)

We can see that once the file is edited a message appears indicating that there is no crontab for the root user and an empty one has been used.

![Info about there is no crontab for the root user](/img/LINUX/LinuxL02/Task01_14_crontab_info.png)

If we check the file /etc/crontab we see that the line has not been added.

![See that line not added in /etc/crontab](/img/LINUX/LinuxL02/Task01_15_cat_crontab.png)

The reason is the following:

The crontab -e command and the /etc/crontab file are two different ways of managing cron jobs, and they do not synchronize with each other.

When we use crontab -e, we are editing a cron table specific to the current user. These user cron tables are stored in a different location (usually in /var/spool/cron/cron/crontabs/) and do not affect the /etc/crontab file.

On the other hand, the /etc/crontab file is a system cron table that can contain cron jobs for multiple users. This file is managed directly and is not affected by crontab -e commands from individual users.

Therefore, when adding a job using crontab -e as the root user, we do not see that job in the /etc/crontab file because they are managed independently.

If we do a cat to the /var/spool/cron/root directory we do see the added line.

![See cron root](/img/LINUX/LinuxL02/Task01_16_cat_var_spool_cron_root.png)
