# Linux Level 2

## Task 14 - Linux Postfix Mail Server

#### xFusionCorp Industries has planned to set up a common email server in Stork DC. After several meetings and recommendations they have decided to use postfix as their mail transfer agent and dovecot as an IMAP/POP3 server. We would like you to perform the following steps:

#### 1. Install and configure postfix on Stork DC mail server.

#### 2. Create an email account jim@stratos.xfusioncorp.com identified by TmPcZjtRQx.

#### 3. Set its mail directory to /home/jim/Maildir.

#### 4. Install and configure dovecot on the same server.

We will connect to the mail server via SSH.

![ssh connect](/img/LINUX/LinuxL02/Task14_01_ssh.png)

Then we will switch to the root user.

```bash
$ sudo su
```

![Change to root](/img/LINUX/LinuxL02/Task14_02_sudo_su.png)

After we will update the installed packages.

```
# yum update -y
```

![Update packages](/img/LINUX/LinuxL02/Task14_03_yum_update.png)

When finished, we will install postfix.

```
# yum install -y postfix
```

![Postfix install](/img/LINUX/LinuxL02/Task14_04_yum_install.png)

Once the installation is finished, edit the `/etc/postfix/main.cf` file that contains the Postfix configuration.

We must make the following changes.

- Locate the line _myhostname_ in the section _INTERNET HOST AND DOMAIN NAMES_. Then uncomment it and modify _host.domain.ltd_ by our host and domain.

- Find the _mydomain_ line, uncomment it, and add our domain.

- In the section _SENDING MAIL_ uncomment the line _myorigin = $mydomain_.

- In the section _RECEIVING MAIL_ uncomment the line _inet_interfaces = all_ and comment the line _inet_interfaces = localhost_.

- Then find the line _mydestination_. We must leave the first line commented out and the second uncomment it.

- Then in the section _DELIVERY TO MAILBOX_ uncomment _home_mailbox = Maildir/_.

All these changes are shown in the following images.

![Edit etc/postfix/main.cf](/img/LINUX/LinuxL02/Task14_05_maincf.png)

![Edit etc/postfix/main.cf](/img/LINUX/LinuxL02/Task14_06_maincf_2.png)

![Edit etc/postfix/main.cf](/img/LINUX/LinuxL02/Task14_07_maincf_3.png)

![Edit etc/postfix/main.cf](/img/LINUX/LinuxL02/Task14_08_maincf_4.png)

Once edited, save and exit.

Next, let's start the postfix service and check that it starts and there are no errors.

```
# systemctl start postfix

# systemctl status postfix
```

![Start postfix](/img/LINUX/LinuxL02/Task14_09_start_status_postfix.png)

As we can see, we have started it but not enabled it, it is disabled. To start it when the server is restarted, we will execute the following commands.

```
# systemctl enable postfix

# systemctl status postfix
```

![Enable postfix](/img/LINUX/LinuxL02/Task14_10_enable_status_postfix.png)

Now we are going to create the user requested by the task and we will assign the indicated password.

![Add user](/img/LINUX/LinuxL02/Task14_11_add_user.png)

To test the operation of postfix we will Telnet to port 25. This port is used by the SMTP protocol. If there is a connection, we will send an email to the user created earlier.

```
# telnet stmail01 25

EHLO localhost
mail from:jim@stratos.xfusioncorp.com
rcpt to:jim@stratos.xfusioncorp.com
DATA
test mail
quit
```

![Telnet 25](/img/LINUX/LinuxL02/Task14_12_telnet.png)

As we can see, we have had connection with our host on port 25 and apparently we have been able to send the mail. If we look at it, it appears queued as 07CD8679B1C6.

The next step is to verify that the mail has been sent, for which we will change the user, from root to jim, and execute the `mailq` command. This command shows us the mail queue.

To change the user, we use the command `su` followed by the user name.

![Switch to jim](/img/LINUX/LinuxL02/Task14_13_su.png)

As we can see, there is no sized mail. If an email appears, it means that we have done something wrong in the configuration of the main file. The IP or the domain may not be set correctly.

Let's list the jim home to see if the Maildir folder we configured in postfix has been created. We see that the folder has been created, that is a good sign.

![List home](/img/LINUX/LinuxL02/Task14_14_ls.png)

If we access the Maildir directory and list the contents, we will see a new folder.

![List Maildir](/img/LINUX/LinuxL02/Task14_15_ls.png)

Si listamos el contendio de new, veremos un fichero que es el correo enviado anteriormente. Si hacemos un cat a ese fichero veremos el contenido.

![List new](/img/LINUX/LinuxL02/Task14_155_ls.png)

Having checked the correct operation, we are going to install the dovecot package, which is an IMAP and POP3 server.

```
# yum install -y dovecot
```

![Install dovecot](/img/LINUX/LinuxL02/Task14_16_install_dovecot.png)

After installing the package, we will edit the `/etc/dovecot/dovecot.conf` file. This is the main Dovecot configuration file.

In this file we must uncomment the line _protocols = imap pop3 lmtp submission_.

![Edit dovecot config](/img/LINUX/LinuxL02/Task14_17_dovecotconf.png)

![Edit dovecot config](/img/LINUX/LinuxL02/Task14_18_dovecotconf.png)

- Uncomment the line _disable_plaitext_auth = yes_. This line indicates that Dovecot will fail authentication if the client does not use SSL or does not use non-plaintext authentication.

- In line _auth_mechanisms = plain_ add login. This line enables the PLAIN and LOGIN authentication mechanisms.

![Edit dovecot config](/img/LINUX/LinuxL02/Task14_19_mailconf.png)

![Edit dovecot config](/img/LINUX/LinuxL02/Task14_20_authconf.png)

![Edit dovecot config](/img/LINUX/LinuxL02/Task14_21_authconf.png)

Once the previous file has been edited, we will modify the `/etc/dovecot/conf.d/10-master.conf` file. This contains settings that will be used by dovecot.

Here we should look for _unix_listener auth-userdb_ and uncomment _user_ and _group_ and add in both postfix.

![Edit dovecot config](/img/LINUX/LinuxL02/Task14_22_masterconf.png)

![Edit dovecot config](/img/LINUX/LinuxL02/Task14_23_masterconf.png)

Once the files have been edited, we start the dovecot service

```
# systemctl start dovecot

# systemctl status dovecot
```

![Start dovecot](/img/LINUX/LinuxL02/Task14_24_start_dovecot.png)

We enable it to start when we start the server.

![Enable dovecot](/img/LINUX/LinuxL02/Task14_25_enabledovecot.png)

```
# systemctl enable dovecot
```

To finish, we will do a verification. We will launch a telnet to port 110 (used by the POP3 protocol) to verify the connection, we will connect with the user jim and his password, and we will see the mail sent previously.

```
# telnet stmail01 110
user jim
pass {given-password}
retr 1
quit
```

![Telnet 110](/img/LINUX/LinuxL02/Task14_26_telnet.png)

With the above we have verified that the dovecot configuration is correct.
