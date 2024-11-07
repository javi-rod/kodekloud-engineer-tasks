# Linux Level 2

## Task 2 – Linux Banner

#### During the monthly compliance meeting, it was pointed out that several servers in the Stratos DC do not have a valid banner. The security team has provided serveral approved templates which should be applied to the servers to maintain compliance. These will be displayed to the user upon a successful login.

#### Update the message of the day on all application and db servers for Nautilus. Make use of the approved template located at /home/thor/nautilus_banner on jump host

The first thing we are going to do is to visualize the content of the banner.

```bash
cat /home/thor/nautilus_banner
```

![See banner template](/img/LINUX/LinuxL02/Task02_01_banner_template.png)

Then we open another terminal and connect to one of the servers and edit the file /etc/motd. That file is the one that we must edit to include a message or banner once the session is started.

Once connected to the server we will visualize if it has some banner.

```bash
$ cat /etc/motd
```

![View de motd file](/img/LINUX/LinuxL02/Task02_02_cat_etc_motd.png)

As we can see it does not have any.

We edit the file with sudo because it requires privileges

```bash
$ sudo vi /etc/motd
```

![Edit motd file](/img/LINUX/LinuxL02/Task02_03_vi_etc_motd.png)

We copy the content of the banner of the jump computer to the file and save and exit.

![Add banner](/img/LINUX/LinuxL02/Task02_04_banner.png)

To verify that it was saved correctly we visualize again the content of the /etc/motd file.

```bash
$ cat /etc/motd
```

These steps must be performed on each server.
