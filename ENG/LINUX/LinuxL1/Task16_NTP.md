# Linux Level 1

## Task 16 - Linux NTP Setup

#### The system admin team of xFusionCorp Industries has noticed an issue with some servers in Stratos Datacenter where some of the servers are not in sync w.r.t time. Because of this, several application functionalities have been impacted. To fix this issue the team has started using common/standard NTP servers. They are finished with most of the servers except App Server 2. Therefore, perform the following tasks on this server:

#### 1. Install and configure NTP server on App Server 2.

#### 2. Add NTP server 1.my.pool.ntp.org in NTP configuration on App Server 2.

#### 3. **Please do not try to start/restart/stop ntp service**, as we already have a restart for this service scheduled for tonight and we don't want these changes to be applied right now.

The first thing we will do is to change to the root user to avoid using sudo.

```bash
$ sudo su
```

Now let's install ntp

```
# yum install ntp
```

![sudo su command](/img/LINUX/LinuxL01/Task16_01_sudo_su.png)

Once installed, we enable it

```
# yum systemctl enable ntpd
```

![sytemctl command](/img/LINUX/LinuxL01/Task16_02_systemctl.png)

If we look at the status, it appears loaded but inactive, as requested.

```
# yum systemctl status ntpd
```

![systemctl command](/img/LINUX/LinuxL01/Task16_03_systemctl.png)

To add the new server, we will edit the file /etc/ntp.conf

```
# vi /etc/ntp.conf
```

![vi command](/img/LINUX/LinuxL01/Task16_04_vi.png)

![edit file](/img/LINUX/LinuxL01/Task16_05_vi.png)
