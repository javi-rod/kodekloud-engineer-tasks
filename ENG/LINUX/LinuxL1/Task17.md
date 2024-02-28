# Linux Level 1

## Task 17 - Linux Firewalld Rules

#### The Nautilus system admins team recently deployed a web UI application for their backup utility running on the Nautilus backup server in Stratos Datacenter. The application is running on port 8088. They have firewalld installed on that server. The requirements that have come up include the following:

#### Open all incoming connection on 8088/tcp port. Zone should be public.

To carry out this exercise we can rely on the documentation https://firewalld.org/documentation/.

Once connected to the server, we will switch to the root user and then we will see the firewall status.

```
# systemctl status firewalld
```

![ssh connect, change to root user and exec systemctl](/img/LINUX/LinuxL01/Task17_01_ssh.png)

We will check the areas we have at our disposal

```
# firewall-cmd --get-zones
```

![view zones of FW](/img/LINUX/LinuxL01/Task17_02_firewallcmd.png)

To create the indicated rule, we must execute the following command

```
# firewall-cmd --permanent --zone=public --add-port= 8088/tcp
```

![add rule](/img/LINUX/LinuxL01/Task17_03_firewallcmd.png)

Now we must reload the configuration

```
# firewall-cmd reload
```

![reload FW](/img/LINUX/LinuxL01/Task17_04_firewallcmd.png)

And finally we will check that the rule was added

```
# firewall-cmd --list-ports
```

![view ports](/img/LINUX/LinuxL01/Task17_05.png)
