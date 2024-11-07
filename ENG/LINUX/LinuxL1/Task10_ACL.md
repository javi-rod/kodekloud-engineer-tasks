# Linux Level 1

## Task 10 - Linux Access Control List

#### The Nautilus security team performed an audit on all servers present in Stratos DC. During the audit some critical data/files were identified which were having the wrong permissions as per security standards. Once the report was shared with the production support team, they started fixing the issues one by one. It has been identified that one of the files named /etc/hosts on Nautilus App 2 server has wrong permissions, so that needs to be fixed and the correct ACLs needs to be set.

#### 1. The user owner and group owner of the file should be root user.

#### 2. Others must have read only permissions on the file.

#### 3. User javed must not have any permission on the file.

#### 4. User eric should have read only permission on the file.

To view the ACL of the /etc/hosts file, use the following command

```bash
$ getfacl /etc/hosts
```

As we can see the owner and group are correct. Others have the read permission. Therefore points 1 and 2 are ok.

![getfacl  command](/img/LINUX/LinuxL01/Task10_01_getfacl.png)

For point 3 we will execute the following command, this allows us to modify the ACL in /etc/host. The -m option is used to indicate that we are going to modify the ACL of a file or directory. The -u option is used to indicate that we are modifying the permissions of a user. After the user we indicate the permissions that it must have, in this case as it must not have we use ---

```bash
$ sudo setfacl -m u:javed:--- /etc/hosts
```

![sudo setfacl command](/img/LINUX/LinuxL01/Task10_02_sudo_setfacl.png)

For point 4, we use the same command as above, except that in the permissions we indicate r since we want it to be able to read the file.

```bash
$ sudo setfacl -m u:eric:r /etc/hosts
```

![sudo setfacl command](/img/LINUX/LinuxL01/Task10_03_sudo_setfacl.png)

If we now review the ACL, we will see that the users with their respective permissions have been added.

```bash
$ getfacl /etc/hosts
```

![comando getfacl](/img/LINUX/LinuxL01/Task10_04_getfacl.png)
