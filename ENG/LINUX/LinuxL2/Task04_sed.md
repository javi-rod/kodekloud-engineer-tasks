# Linux Level 2

## Task 4 - Linux String Substitute (sed)

#### There is some data on Nautilus App Server 2 in Stratos DC. Data needs to be altered in several of the files. On Nautilus App Server 2, alter the /home/BSD.txt file as per details given below:

#### a. Delete all lines containing word code and save results in /home/BSD_DELETE.txt file. (Please be aware of case sensitivity)

#### b. Replace all occurrence of word and to them and save results in /home/BSD_REPLACE.txt file.

#### Note: Let's say you are asked to replace word to with from. In that case, make sure not to alter any words containing the string itself; for example up**to**, contribu**to**r etc.

Although it is not necessary for this exercise, it is good practice to make a copy of the file to edit. We will use sudo since our user does not have write permission in the /home directory.

```bash
$ sudo cp /home/BSD.txt /home/BSD.txt.copy
```

![Backup file BSD.txt](/img/LINUX/LinuxL02/Task04_01_sudo_cp.png)

To check that the file has been copied we will list the /home directory

```bash
$ ls -al /home/
```

![List directory](/img/LINUX/LinuxL02/Task04_02_ls.png)

Now let's look at the code matches in the file

```bash
$ cat /home/BSD.txt | grep code
```

![See code matches](/img/LINUX/LinuxL02/Task04_03_cat.png)

To count the number of times it appears we execute the previous command adding an | and the command wc -l

![Count number of code occurrences](/img/LINUX/LinuxL02/Task04_04_cat.png)

To continue, let's switch to the root user.

```bash
$ sudo su
```

![Change to root](/img/LINUX/LinuxL02/Task04_05_sudo_su.png)

Next, we will delete the lines containing the word code and create a new file with the result.

```
# sed '/code/d' /home/BSD.txt > /home/BSD_DELETE.txt
```

`'/code/d'`: It is the expression that sed is going to execute. The slash / is used to delimit a regular expression (in this case, the word 'code'). The d at the end is a command that tells sed to delete the lines that match the regular expression.

![Delete lines containing code and create new file](/img/LINUX/LinuxL02/Task04_06_sed.png)

Then we will list the /home directory to see that the file has been created.

```
# ls -al /home/
```

![List directory](/img/LINUX/LinuxL02/Task04_07_ls.png)

Once we see that the file has been created, let's see the content.

```
# cat /home/BSD_DELETE.txt
```

![See file content](/img/LINUX/LinuxL02/Task04_08_cat.png)

As we can see there is no longer a point 1 where the word code appeared.

Now we are going to look for matches for and. This time instead of using a cat and concantenate grep, as we have been doing before, we are going to run just grep.

```
# grep and /home/BSD.txt
```

![See matches and](/img/LINUX/LinuxL02/Task04_09_grep.png)

After seeing the matches we will proceed to replace and by them as follows.

```
# sed 's/\<and\>/them/g' /home/BSD.txt > /home/BSD_REPLACE.txt
```

`'s/\<and\>/them/g'`: This is the argument we pass to sed. s is the replace command. \<and> is the word we want to replace (the use of \<and> ensures that it is treated as a complete word and not as part of another word). them is the word we want to replace and with. g is a flag indicating that we want to replace all occurrences of and on each line, not just the first one.

![Change and to them and create new file](/img/LINUX/LinuxL02/Task04_10_sed.png)

If we look at the number of appearances of and we see that the result is 24.

```
# grep and /home/BSD.txt | wc -l
```

![View number of matches for and](/img/LINUX/LinuxL02/Task04_11_grep.png)

Let us now compare the previous result with the number of occurrences of them in the new file.

```
# grep and /home/BSD_REPLACE.txt | wc -l
```

![View number of matches for them](/img/LINUX/LinuxL02/Task04_12_grep.png)

As we can see both show the same number of occurrences, 24.

To finish, let's see the matches of them in the file /home/BSD_REPLACE.txt

```
# cat /home/BSD_REPLACE.txt
```

![See them matches](/img/LINUX/LinuxL02/Task04_13_grep.png)
