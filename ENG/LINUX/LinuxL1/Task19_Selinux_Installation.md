# Linux Level 1

## Task 19 - Selinux Installation

#### The xFusionCorp Industries security team recently did a security audit of their infrastructure and came up with ideas to improve the application and server security. They decided to use SElinux for an additional security layer. They are still planning how they will implement it; however, they have decided to start testing with app servers, so based on the recommendations they have the following requirements:

#### Install the required packages of SElinux on App server 3 in Stratos Datacenter and disable it permanently for now; it will be enabled after making some required configuration changes on this host. Don't worry about rebooting the server as there is already a reboot scheduled for tonight's maintenance window. Also ignore the status of SElinux command line right now; the final status after reboot should be **disabled**.

First we will switch to root

```bash
$ sudo su
```

![comando sudo su](/img/LINUX/LinuxL01/Task19_01_sudo_su.png)

We update the installed packages

```
# yum update
```

![comando yum update](/img/LINUX/LinuxL01/Task19_02_yum_update.png)

Once we are done, we will install the necessary packages for SELinux

```
# yum install policycoreutils selinux-policy selinux-policy-targeted
```

![comando yum install](/img/LINUX/LinuxL01/Task19_03_yum_install.png)

When finished we can see the status of SELinux

```
# sestatus
```

As we can see, it appears as disabled. This is the current status.

![comando sestatus](/img/LINUX/LinuxL01/Task19_04_sestatus.png)

To view its configuration we must check the file /etc/selinux/config

```
vi /etc/selinux/config
```

As we can see SELINUX is in enforcing and we are asked to leave it disabled. Let's change it to disabled and save it.

![editar configuración selinux](/img/LINUX/LinuxL01/Task19_05_selinux_conf.png)
