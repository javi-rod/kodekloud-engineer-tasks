# Linux Level 1

## Task 14 - Linux - Run Levels

#### New tools have been installed on the app servers in Stratos Datacenter. Some of these tools can only be managed from the graphical user interface. Therefore, there are some requirements for these app servers as below.

#### On all App servers in Stratos Datacenter, change the default runlevel so that they can boot in GUI (graphical user interface) by default. **Please do not try to reboot these servers after completing this task.**

Runlevels are used in sysV init while in systemd init are systemd targets.

To find out if our system uses sysV init or systemd init we will run the following command

```bash
$ ls -l /sbin/init
```

As we can see, our system makes use of systemd

![ls command](/img/LINUX/LinuxL01/Task14_01_ls.png)

If we execute the runlevel command we will see that it returns a number.

```bash
$ runlevel
```

![runlevel command](/img/LINUX/LinuxL01/Task14_02_runlevel.png)

That runlevel 3 indicates that it is currently running in command line.

As we are in systemd init we use systemd targets and to see which one is being used in the default startup we must run

```bash
$ systemctl get-default
```

![systemctl command](/img/LINUX/LinuxL01/Task14_03_systemctl.png)

multi-user.target means that it starts in command line mode.

To modify it we must change it to graphical.target as follows.

```bash
$ sudo systemctl set-default graphical.target
```

![systemctl command](/img/LINUX/LinuxL01/Task14_04_systemctl.png)

If we check again that systemd target is now set by default, we will see that it has changed, now it will boot in graphical mode.

```bash
$ systemctl get-default
```

![systemctl command](/img/LINUX/LinuxL01/Task14_05_systemctl.png)
