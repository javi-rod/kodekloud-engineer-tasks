# Linux Level 2

## Task 8 - Install Ansible

#### During the weekly meeting, the Nautilus DevOps team discussed about the automation and configuration management solutions that they want to implement. While considering several options, the team has decided to go with Ansible for now due to its simple setup and minimal pre-requisites. The team wanted to start testing using Ansible, so they have decided to use jump host as an Ansible controller to test different kind of tasks on rest of the servers.

#### Install ansible version 4.9.0 on Jump host using pip3 only. Make sure Ansible binary is available globally on this system, i.e all users on this system are able to run Ansible commands.

To do this exercise we can use the following documentation:

https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-and-upgrading-ansible-with-pip

Install Ansible version 4.9.0 with the following command

```bash
$ sudo pip3 install ansible==4.9.0
```

![Install Ansible](/img/LINUX/LinuxL02/Task08_01_pip3.png)

Once installed, we are going to verify that it works, for them we test to see the installed version executing the following command.

```bash
$ ansible --version
```

![Verify Ansible version](/img/LINUX/LinuxL02/Task08_02_ansible_version.png)

Now let's check if Ansible is in the PATH. If we look at the previous image, we will see that the executable is in /usr/local/bin and that directory is in the PATH.

![View PATH variable](/img/LINUX/LinuxL02/Task08_03_path.png)
