# Ansible Repo

**This repo is WIP**

**Purpose:** To automate patch management of Linux and Windows operating systems and respective applications using Ansible and Chocolatey

Make sure you have:
* A Linux machine or Linux VM to download and store these files (will be referred to as the Linux admin machine)
* Have ansible installed on that Linux admin machine
* Machines that need regular patching that are Windows and/or Linux machines (will be referred to as the host machines)
* If its a Windows machine, configured winrm on the host machines
* If its a Linux machine, configured ssh on the host machines

The instructions below are assuming that the playbooks have worked before and you are looking to configure a new admin machine:

1) Download and store the repo files in /etc/ansible
2) List/Replace the machines on your network by IP addresses and group them by operating system
3) Store the password of the admin Windows user in the ansible vault
4) Store the output of the ansible vault in the windows.yml file under /etc/ansible/group_vars
5) Write the password of the ansible vault in the open_vault.txt file
6) create ssh keys for the Linux admin machine
7) copy the ssh keys onto the host Linux machines
8) check that the Linux admin machine can connect to the host machines using "ansible -m ping linux" and "ansible -m win_ping windows"
9) Run chocolatey-install.yml playbook using the command "ansible-playbook /etc/ansible/playbooks/chocolatey-install.yml" (customize this file and all subsequent .yml files to your liking. For me, it includes Chocolately, Chocolatey GUI, and packages)
10) Run update-all.yml playbook using the command "ansible-playbook /etc/ansible/playbooks/update-all.yml" (Windows computers will automatically restart and reconnect to check in, if needed for OS updates)
11) Run win-reboot.yml playbook using the command "ansible-playbook /etc/ansible/playbooks/win-reboot.yml" to restart all Windows computers (good idea after updates)
12) Run win-shutdown.yml playbook using the command "ansible-playbook /etc/ansible/playbooks/win-shutdown.yml" to shutdown all Windows computers (if desired)
