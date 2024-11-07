# Linux Level 2

## Task 13 - Linux Firewalld Setup

#### To secure our Nautilus infrastructure in Stratos Datacenter we have decided to install and configure firewalld on all app servers. We have Apache and Nginx services running on these apps. Nginx is running as a reverse proxy server for Apache. We might have more robust firewall settings in the future, but for now we have decided to go with the given requirements listed below:

#### a. Allow all incoming connections on Nginx port, i.e 80.

#### b. Block all incoming connections on Apache port, i.e 8080.

#### c. All rules must be permanent.

#### d. Zone should be public.

#### e. If Apache or Nginx services aren't running already, please make sure to start them.

In each of the servers we will have to perform the following steps.

First, update packages.

```bash
$ sudo yum update -y
```

![Update packages](/img/LINUX/LinuxL02/Task13_01_update.png)

Once updated, we proceed to install `firewalld`.

```bash
$ sudo yum install -y firewalld
```

![Install firewalld](/img/LINUX/LinuxL02/Task13_02_install_firewalld.png)

Once the installation is finished, we will see the status of the service.

```bash
$ systemctl status firewalld
```

![firewalld status](/img/LINUX/LinuxL02/Task13_03_status_fw.png)

As we can see, the service is not started. To start the service we must execute the following.

```bash
$ sudo systemctl start firewalld
```

Now we check again if it is already started.

```bash
$ systemctl status firewalld
```

![firewalld status](/img/LINUX/LinuxL02/Task13_04_status_fw.png)

We see that it is already started, so we proceed with the requested configuration. First we switch to the root user.

```bash
$ sudo su
```

Let's see what ports we have open in the public area.

```
# firewall-cmd --zone=public --list-all
```

![View public zone config](/img/LINUX/LinuxL02/Task13_05_list_zone_public.png)

As we can see there are no ports allowed. Let's add port 80 as requested.

```
# firewall-cmd --permanent --zone=public --add-port=80/tcp
```

![Add port](/img/LINUX/LinuxL02/Task13_06_add_port.png)

Once added, we reload the configuration.

```
# firewall-cmd --reload
```

![Reload config](/img/LINUX/LinuxL02/Task13_07_reload_conf.png)

If we check the public zone configuration again, we can see that port 80 is now displayed.

```
# firewall-cmd --zone=public --list-all
```

![View public zone config](/img/LINUX/LinuxL02/Task13_08_list_zone.png)

We do not have to do any more in terms of Firewall, since the ports are closed and 8080 must remain closed. There are no blocks here, only permissions to add.

Before finishing, we will check if Apache and Nginx are running.

```
# systemctl status httpd

# systemctl status nginx
```

![Apache and Nginx status](/img/LINUX/LinuxL02/Task13_09_status_httpd_nginx.png)
