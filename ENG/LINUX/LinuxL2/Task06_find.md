# Linux Level 2

## Task 6 - Linux Find Command

#### During a routine security audit, the team identified an issue on the Nautilus App Server. Some malicious content was identified within the website code. After digging into the issue they found that there might be more infected files. Before doing a cleanup they would like to find all similar files and copy them to a safe location for further investigation. Accomplish the task as per the following requirements:

#### a. On App Server 3 at location /var/www/html/blog find out all files (not directories) having .php extension.

#### b. Copy all those files along with their parent directory structure to location /blog on same server.

#### c. Please make sure not to copy the entire /var/www/html/blog directory content.

We will connect via SSH to the corresponding server, in this case APP Server 3.

```bash
$ ssh banner@172.16.238.12
```

![Connect to server](/img/LINUX/LinuxL02/Task06_01_ssh.png)

Once connected, we are going to make a search with the command find passing in addition the command wc with the option -l, this allows us to see the number of files with php extension.

```bash
$ find /var/www/html/blog -type f -name '*.php' | wc -l
```

![Search and count of occurrences](/img/LINUX/LinuxL02/Task06_02_find_wc.png)

As we can see, we have 1077 php files.

Now we are going to look for the files again and copy them in the directory indicated in the exercise, taking into account that we have to respect the structure. We will use the sudo command to copy the files to the destination.

```bash
$ sudo find /var/www/html/blog -type f -name "*.php" -exec bash -c 'dir="/blog/$(dirname "{}")"; mkdir -p "$dir"; cp "{}" "$dir"' \;
```

Below is a more detailed explanation of what the command does.

• find /var/www/html/blog -type f -name "\*.php": With this we search for all files (not directories) with extension .php in the directory /var/www/html/blog.

• -exec bash -c '...' \;: This option tells find to execute the command specified in '...' for each file found. The ; at the end indicates the end of the -exec command.

• 'dir="/blog/$(dirname "{}")"; mkdir -p "$dir"; cp "{}" "$dir"': This is the command that is executed for each file found. Here, {} is a placeholder that find replaces with the name of each file found.

- dir="/blog/$(dirname "{}")": Here, dirname "{}" gets the directory name of the current file, and then concatenates with "/blog/" to get the path to the destination directory. The result is stored in the variable dir.

- mkdir -p "$dir": Este comando crea el directorio de destino (y cualquier directorio padre necesario) si no existe.

- cp "{}" "$dir": This command creates the target directory (and any necessary parent directory) if it does not exist.

![Search and copy files](/img/LINUX/LinuxL02/Task06_03_find_exec.png)

If we now list the contents of the /blog/var/html/blog/ directory we will see the copied files as well as the directories of the structure.

![List directory](/img/LINUX/LinuxL02/Task06_04_ls.png)

To verify that they have all been copied, execute the following command

```bash
$ find /blog -type f -name '*.php' | wc -l
```

![Search and count of occurrencess](/img/LINUX/LinuxL02/Task06_05_find_wc.png)

As we can see, the same number of files appears.
