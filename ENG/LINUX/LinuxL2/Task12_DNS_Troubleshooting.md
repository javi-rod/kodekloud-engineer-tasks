# Linux Level 2

## Task 12 - DNS Troubleshooting

#### The system admins team of xFusionCorp Industries has noticed intermittent issues with DNS resolution in several apps . App Server 2 in Stratos Datacenter is having some DNS resolution issues, so we want to add some additional DNS nameservers on this server.

#### As a temporary fix we have decided to go with Google public DNS (ipv4). Please make appropriate changes on this server.

Once we have connected to the App Server 2 server we are going to make a copy of the file `/etc/resolv.conf`

This file contains the DNS we are going to use.

```bash
$ sudo cp /etc/resolv.conf /etc/resolv.conf.backup
```

![Backup copy of resolv.conf file](/img/LINUX/LinuxL02/Task12_01_sudo_cp.png)

Once we have a copy, we edit the file and add the Google DNS (8.8.8.8.8 and 8.8.4.4)

```bash
$ sudo vi /etc/resolv.conf
```

![Add Google DNS](/img/LINUX/LinuxL02/Task12_02_resolvconf.png)

Save and exit. And with this we would have completed the exercise.

If we restart the network service we will receive an error. Do not worry, this error was already present at the beginning of the exercise.

```bash
$ sudo systemctl restart network.service
```

![Restart network service](/img/LINUX/LinuxL02/Task12_03_sudo_systemctl_restart.png)

```bash
$ sudo systemctl status network.service
```

![View network service status](/img/LINUX/LinuxL02/Task12_04_sudo_systemctl_status.png)

We can run the indicated command, journalctl, which collects and manages the system logs. This way we can see in more detail what is happening.

```bash
$ sudo journalctl -xe
```

![Check error](/img/LINUX/LinuxL02/Task12_05_sudo_journal.png)

If we run `ip address` we can see if the interfaces are up, as you can see everything is up.

![View interfaces](/img/LINUX/LinuxL02/Task12_06_ip_address.png)

If we do a `ping` to the google DNS servers we see that they respond.

![Connection test](/img/LINUX/LinuxL02/Task12_07_ping.png)
