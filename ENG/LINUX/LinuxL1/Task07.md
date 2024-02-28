# Linux Level 1

## Task 7 - Disable Root Login

#### After doing some security audits of servers, xFusionCorp Industries security team has implemented some new security policies. One of them is to disable direct root login through SSH.

#### Disable direct SSH root login on all app servers in Stratos Datacenter.

The following steps will be performed on all the application servers in the organization

First, we go to the directory /etc/ssh and list the content

```bash
$ cd /etc/ssh
```

```bash
$ ls -al
```

![cd command](/img/LINUX/LinuxL01/Task07_01_cd.png)

As we can see, there is the SSH configuration file (sshd_config) that we will edit with the vi command. If we are not root we will have to execute it with the sudo command.

```bash
$ sudo vi sshd_config
```

![sudo vi command](/img/LINUX/LinuxL01/Task07_02_sudo_vi.png)

Once the file is opened, go to the Authentication section and change the value of PermitRootLogin from yes to no. After editing, save and close the file.

![sshd_config file](/img/LINUX/LinuxL01/Task07_03_auth.png)

Now it is time to restart the service to take the new configuration.

```bash
$ sudo systemctl restart sshd.service
```

![sudo systemctl command](/img/LINUX/LinuxL01/Task07_04_sudo_systemctl.png)
