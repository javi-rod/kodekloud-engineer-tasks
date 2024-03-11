# Linux Level 2

## Task 5 - Linux SSH Authentication

#### The system admins team of xFusionCorp Industries has set up some scripts on jump host that run on regular intervals and perform operations on all app servers in Stratos Datacenter. To make these scripts work properly we need to make sure the thor user on jump host has password-less SSH access to all app servers through their respective sudo users (i.e tony for app server 1). Based on the requirements, perform the following:

#### Set up a password-less authentication from user thor on jump host to all app servers through their respective sudo users.

To perform this task we need to generate a pair of keys. One private and one public. The private key will remain on the jump server, while the public key will be copied to the application servers.

The command we will use to perform this step is `ssh-keygen`. This command is used for generation, management and conversion of authentication keys.

We will use the -t option to indicate the type of key to use, in this case rsa.

```bash
$ ssh-keygen -t rsa
```

![Create keys](/img/LINUX/LinuxL02/Task05_01_ssh_keygen.png)

If we list the contents of the /home/thor/.ssh directory we see that two files have been generated, `id_rsa` and `id_rsa.pub`.

These two files are the private and public keys.

```bash
$ ls -al /home/thor/.ssh
```

![Public and Private Keys](/img/LINUX/LinuxL02/Task05_02_claves.png)

To copy the public key and be able to access without credentials, we will use the command ssh-copy-id. We must specify the user we will use to connect and the IP of the server. This command will copy the public key to the remote server and add it to the ~/.ssh/authorized_keys file of the remote user.

```bash
$ ssh-copy-id tony@172.16.238.10
```

![Copy keys](/img/LINUX/LinuxL02/Task05_03_ssh_copy_tony.png)

Now we will test the access to the server, with the user tony to verify that it does not request the password.

![Check access](/img/LINUX/LinuxL02/Task05_04_ssh_tony.png)

Now we are going to copy the keys to the other two servers.

![Copy keys](/img/LINUX/LinuxL02/Task05_05_ssh_copy_steve_banner.png)

Once done, we check that we are accessing without user credentials.

![Check access](/img/LINUX/LinuxL02/Task05_06_ssh_steve_banner.png)
