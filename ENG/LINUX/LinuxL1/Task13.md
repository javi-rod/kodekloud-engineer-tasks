# Linux Level 1

## Task 13 - Cron schedule deny to users

#### To stick with the security compliances, the Nautilus project team has decided to apply some restrictions on crontab access so that only allowed users can create/update the cron jobs. Limit crontab access to below specified users on App Server 3.

#### Allow crontab access to john user and deny the same to eric user.

To allow or deny access you need two files, cron.allow and cron.deny inside the /etc directory.

First we will check if those files exist, for which we will list the content in /etc that begins with cron.

```bash
$ ls -al /etc/cron*
```

![ls command](/img/LINUX/LinuxL01/Task13_01_ls.png)

As we can see, the two files do not exist, so we will create them as follows

```bash
$ sudo vi /etc/cron.allow
```

In this file we will add the user who must have permission, in this case john

![sudo vi command](/img/LINUX/LinuxL01/Task13_02_sudo_vi.png)

![vi editor](/img/LINUX/LinuxL01/Task13_03_vi.png)

```bash
$ sudo vi /etc/cron.deny
```

In this file we will add the user that should not have permission, in this case eric.

![sudo vi command](/img/LINUX/LinuxL01/Task13_04_sudo_vi.png)

![vi editor](/img/LINUX/LinuxL01/Task13_05_vi.png)

Once these files with the users have been created, if we make a list as above we will see that both files are already present.

```bash
$ ls -al /etc/cron*
```

![ls command](/img/LINUX/LinuxL01/Task13_06_ls.png)

Now we restart the service

```bash
$ sudo systemctl restart crond.service
```

We check that it is running

```bash
$ sudo systemctl status crond.service
```

![sudo systemctl command](/img/LINUX/LinuxL01/Task13_07_sudo_systemctl.png)

If we now check the permissions we see that john does not have permission.

![sudo crontab command](/img/LINUX/LinuxL01/Task13_08_sudo_crontab.png)

This is because there is no crontab file, there are no cron jobs for the user.
