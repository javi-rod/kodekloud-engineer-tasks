# Linux Level 1

## Task 18 - Linux Resource Limits

#### On our Storage server in Stratos Datacenter we are having some issues where nfsuser user is holding hundred of processes, which is degrading the performance of the server. Therefore, we have a requirement to limit its maximum processes. Please set its maximum process limits as below:

#### a. soft limit = 1026

#### b. hard_limit = 2024

To perform this task we must edit the file /etc/security/limits.conf as follows.

```bash
$ sudo vi /etc/security/limits.conf
```

![comando sudo vi](/img/LINUX/LinuxL01/Task18_01_sudo_vi.png)

![añadir limites](/img/LINUX/LinuxL01/Task18_02_limits_conf.png)
