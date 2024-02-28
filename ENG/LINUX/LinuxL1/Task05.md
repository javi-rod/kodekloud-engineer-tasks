# Linux Level 1

## Task 5 - Linux User Expiry

#### A developer named rose has been assigned Nautilus project temporarily as a backup resource. As a temporary resource for this project, we need a temporary user for rose. It’s a good idea to create a user with an expiration date so that the user won't be able to access servers beyond that point.

#### Therefore, create a user named rose on the App Server 3 in Stratos Datacenter. Set expiry date to 2021-04-15. Make sure the user is created as per standard and is in lowercase.

![ssh command](/img/LINUX/LinuxL01/Task05_01_ssh.png)

Once connected to the server, we will use the useradd command preceded by sudo, requires privileges, and use the -e option to indicate that we want the account to expire on a given date.

```bash
$ sudo useradd -e 2021-04-15 rose
```

![sudo useradd command](/img/LINUX/LinuxL01/Task05_02_sudo_useradd.png)

Now let's verify that the account has been set to expire on the specified date. To do this we will use the chage command. This command is used to modify a user's password expiration data. We will use the -l option to list the user's password information.

```bash
$ sudo chage -l rose
```

![sudo chage](/img/LINUX/LinuxL01/Task05_03_sudo_chage.png)

As we can see in the "Account expieres" section, the date coincides with the value given above.
