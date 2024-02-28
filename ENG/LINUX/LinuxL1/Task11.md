# Linux Level 1

## Task 11 - Linux String Substitute

#### The backup server in the Stratos DC contains several template XML files used by the Nautilus application. However, these template XML files must be populated with valid data before they can be used. One of the daily tasks of a system admin working in the xFusionCorp industries is to apply string and file manipulation commands!

#### Replace all occurances of the string Random to Echo-Location on the XML file /root/nautilus.xml located in the backup server.

To perform this exercise, we are going to use the root user directly to avoid using sudo.

We will execute the following command

```bash
$ sudo su
```

![sudo su command](/img/LINUX/LinuxL01/Task11_01_sudo_su.png)

Once we are root, we are going to see the content of the xml file

```
# cat /root/nautilus.xml
```

As we can see in the tag \<type> appears the word Random that we must replace.

![cat command](/img/LINUX/LinuxL01/Task11_02_cat.png)

With the following command we will know the number of times the word we are looking for appears.

```
# cat /root/nautilus.xml | grep Random | wc -l
```

Now we are going to perform the substitution for them we use the sed command

```
# sed -i 's/Random/Echo-Location/g' /root/nautilus.xml
```

![sed command](/img/LINUX/LinuxL01/Task11_03_sed.png)

-i : In-place editing option. It means that files are edited in place without creating a new file.

- s : Is the substitution command

- g : Is a flag that globally replaces all occurrences of the pattern.

Once we have made the substitution, we must check that the number of occurrences is the same as the one seen previously.

```
# cat /root/nautilus.xml | grep Echo-Location | wc -l
```

![cat command](/img/LINUX/LinuxL01/Task11_04_cat_sed.png)

Once we have made the substitution, we must check that the number of occurrences is the same as the one seen previously.

```
# head /root/nautilus.xml
```

![head command](/img/LINUX/LinuxL01/Task11_05_head.png)
