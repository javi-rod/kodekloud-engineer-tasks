# Linux Level 2

## Task 11 - Linux Configure sudo

#### We have some users on all app servers in Stratos Datacenter. Some of them have been assigned some new roles and responsibilities, therefore their users need to be upgraded with sudo access so that they can perform admin level tasks.

#### a. Provide sudo access to user siva on all app servers.

#### b. Make sure you have set up password-less sudo for the user.

As in the previous exercise, the following steps must be executed in each application server, previously we will have connected via ssh.

Once connected to the server, we change to the root user for convenience. We avoid using sudo in each instruction.

![Change to root user](/img/LINUX/LinuxL02/Task11_01_sudo_su.png)

Next, we are going to allow siva to use sudo without a password. To do this we are going to edit the sudoers file in a secure way with the following command.

![Edit sudoers](/img/LINUX/LinuxL02/Task11_02_visudo.png)

Once the file is opened, we must add these lines `siva ALL=(ALL:ALL) NOPASSWD:ALL` as shown in the image.

![Add line](/img/LINUX/LinuxL02/Task11_03_edit_sudo.png)

Once added, save and exit. And with this you would already have permission.

Another way to do it, would be adding siva to the wheel group. And in the sudoers file indicate `NOPASSWD:ALL` to the group, as I show in the following image.

![Add NOPASSWD:ALL](/img/LINUX/LinuxL02/Task11_04_edit_sudo.png)

This second way is more practical since we control by group and not by user. If we had many users, we would have to put a line for each one.
