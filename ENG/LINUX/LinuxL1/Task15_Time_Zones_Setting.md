# Linux Level 1

## Task 15 - Linux Time Zones Setting

#### During the daily standup, it was pointed out that the timezone across Nautilus Application Servers in Stratos Datacenter doesn't match with that of the local datacenter's timezone, which is Asia/Kathmandu.

#### Correct the mismatch.

If we execute the following command we will see that indeed the time zone is not the one requested.

```bash
$ timedatectl
```

![timedatectl command](/img/LINUX/LinuxL01/Task15_01_timedatectl.png)

To find out which time zones we have in Asia we can run the following command

```bash
$ timedatectl list-timezones | grep Asia
```

![timedatectl command](/img/LINUX/LinuxL01/Task15_02_timedatectl.png)

To establish a new zone, we will execute the following command

```bash
$ sudo timedatectl set-timezone Asia/Kathmandu
```

![timedatectl command](/img/LINUX/LinuxL01/Task15_03_timedatectl.png)

If we launch the timedatectl command again we will see that the time zone has been modified.

```bash
$ timedatectl
```

![timedatectl command](/img/LINUX/LinuxL01/Task15_04_timedatectl.png)
