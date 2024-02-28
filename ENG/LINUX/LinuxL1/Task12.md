# Linux Level 1

## Task 12 - Linux Remote Copy

#### One of the Nautilus developers has copied confidential data on the jump host in Stratos DC. That data must be copied to one of the app servers. Because developers do not have access to app servers, they asked the system admins team to accomplish the task for them.

#### Copy /tmp/nautilus.txt.gpg file from jump server to App Server 2 at location /home/nfsshare.

To make the copy from the jump server to one of the application servers, we have to execute the scp command as follows.

```bash
$ scp /tmp/nautilus.txt.gpg steve@172.16.238.11:/home/nfsshare
```

Now if we connect to the target server via SSH and list the contents of the directory in question, we should see the copied file.

![scp command](/img/LINUX/LinuxL01/Task12_01_scp.png)

![ssh command](/img/LINUX/LinuxL01/Task12_02_ssh.png)
