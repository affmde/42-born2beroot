# <center>Born2beroot - 42 School project</center>
## Description
This is a 42 school project where you learn what are virtual machines, and how to configure it. Virtual box is used for this project.

<br>

# Introduction

## **What is a virtual machine?**
What is a virtual machine?
A Virtual Machine (VM) is a compute resource that uses software instead of a physical computer to run programs and deploy apps. One or more virtual “guest” machines run on a physical “host” machine.  Each virtual machine runs its own operating system and functions separately from the other VMs, even when they are all running on the same host. This means that, for example, a virtual MacOS virtual machine can run on a physical PC. 

Virtual machine technology is used for many use cases across on-premises and cloud environments. More recently, public cloud services are using virtual machines to provide virtual application resources to multiple users at once, for even more cost efficient and flexible compute. 

## **What are virtual machines used for?**
Virtual machines (VMs) allow a business to run an operating system that behaves like a completely separate computer in an app window on a desktop. VMs may be deployed to accommodate different levels of processing power needs, to run software that requires a different operating system, or to test applications in a safe, sandboxed environment.

Virtual machines have historically been used for server virtualization, which enables IT teams to consolidate their computing resources and improve efficiency. Additionally, virtual machines can perform specific tasks considered too risky to carry out in a host environment, such as accessing virus-infected data or testing operating systems. Since the virtual machine is separated from the rest of the system, the software inside the virtual machine cannot tamper with the host computer. 

## **How do virtual machines work?**
The virtual machine runs as a process in an application window, similar to any other application, on the operating system of the physical machine. Key files that make up a virtual machine include a log file, NVRAM setting file, virtual disk file and configuration file. 

## **WHat is LVM?**
LVM stands for Logical Volume Management. It is a system of managing logical volumes, or filesystems, that is much more advanced and flexible than the traditional method of partitioning a disk into one or more segments and formatting that partition with a filesystem.

## **What is AppArmor?**
AppArmor is a Mandatory Access Control (MAC) system which is a kernel (LSM) enhancement to confine programs to a limited set of resources. AppArmor's security model is to bind access control attributes to programs rather than to users. AppArmor confinement is provided via profiles loaded into the kernel, typically on boot. AppArmor profiles can be in one of two modes: enforcement and complain. Profiles loaded in enforcement mode will result in enforcement of the policy defined in the profile as well as reporting policy violation attempts (either via syslog or auditd). Profiles in complain mode will not enforce policy but instead report policy violation attempts.

AppArmor differs from some other MAC systems on Linux: it is path-based, it allows mixing of enforcement and complain mode profiles, it uses include files to ease development, and it has a far lower barrier to entry than other popular MAC systems.

AppArmor is an established technology first seen in Immunix and later integrated into Ubuntu, Novell/SUSE, and Mandriva. Core AppArmor functionality is in the mainline Linux kernel from 2.6.36 onwards; work is ongoing by AppArmor, Ubuntu and other developers to merge additional AppArmor functionality into the mainline kernel.

## **What is the difference between Apt and Aptitute?**
Apt or Advanced Packaging Tool is a free and open source software which gracefully handles software installation and removal. Initially it was designed for Debian’s .deb packages but it has been made compatible with RPM Package Manager.

Apt is whole command line with no GUI. Whenever invoked from command line along with specifying the name of package to be installed, it finds that package in configured list of sources specified in ‘/etc/apt/sources.list’ along with the list of dependencies for that package and sorts them and automatically installs them along with the current package thus letting user not to worry of installing dependencies.

It is highly flexible allowing User to control various configurations easily, like: adding any new source to search for packages, apt-pinning i.e. marking any package unavailable during system up-gradation thus making its current version be its final version installed, “smart” upgrade i.e. upgrading most important packages and leaving the least important ones.

Aptitude is front-end to advanced packaging tool which adds a user interface to the functionality, thus allowing a user to interactively search for a package and install or remove it. Initially created for Debain, Aptitude extends its functionality to RPM based distributions as well.

Its user interface is based on ncurses library which adds various elements to it commonly seen in GUI’s. One of its highlight is that it can emulate most of apt-get’s command line arguments.

In all, Aptitude is a higher-level package managers that abstracts low level details, and can operate in both text-based interactive UI mode and even in command line non-interactive mode.

## **What is SSH and how to use it?**
SSH or Secure Shell is a network communication protocol that enables two computers to communicate (c.f http or hypertext transfer protocol, which is the protocol used to transfer hypertext such as web pages) and share data. An inherent feature of ssh is that the communication between the two computers is encrypted meaning that it is suitable for use on insecure networks.

SSH is often used to "login" and perform operations on remote computers but it may also be used for transferring data.

You use a program on your computer (ssh client), to connect to our service (server) and transfer the data to/from our storage using either a graphical user interface or command line. There are many programs available that enable you to perform this transfer and some operating systems such as Mac OS X and Linux have this capability built in.

SSH clients will typically support SCP (Secure Copy) and/or SFTP (SSH File Transfer Protocol) for transferring data; we tend to recommend using SFTP instead of SCP but both will work with our service.

## **How to implement UFW with SSH**
UFW (Uncomplicated Firewall) is a software application responsible for ensuring that the system administrator can manage iptables in a simple way. Since it is very difficult to work with iptables, UFW provides us with an interface to modify the firewall of our device (netfilter) without compromising security. Once we have UFW installed, we can choose which ports we want to allow connections, and which ports we want to close. This will also be very useful with SSH, greatly improving all security related to communications between devices.

## **What is cron and what is wall?**
Once we know a little more about how to build a server inside a Virtual Machine (remember that you also have to look in other pages apart from this README), we will see two commands that will be very helpful in case of being system administrators. These commands are:

+ **Cron**: Linux task manager that allows us to execute commands at a certain time. We can automate some tasks just by telling cron what command we want to run at a specific time. For example, if we want to restart our server every day at 4:00 am, instead of having to wake up at that time, cron will do it for us.
+ **Wall**: command used by the root user to send a message to all users currently connected to the server. If the system administrator wants to alert about a major server change that could cause users to log out, the root user could alert them with wall.

<br>

# Installation

First you need to get a Debian image. At the time of writing (11/2022), the newest stable version of Debian is 11.5.0. You can get it from [here](https://www.debian.org/distrib/).

<br>

# *sudo*

## Step 1: Installing *sudo*

Switch to root:

    $ su
    $ Password

Install *sudo*
    
    apt install sudo

## Step 2: Add user to sudo group

Add user to sudo group with adduser <username> sudo.

    adduser <username> sudo

or

    sudo usermod -aG sudo <username>

*Notice it can be necessary to use /sbin/usermod*

You can verify if the user was successfuly added to the group by running:

    getent group sudo

Then reboot so that changes can take effect

    sudo reboot

## Step 3: Running root-Privileged Commands
From now on, run root-privileged commands via prefix sudo. For instance:

    sudo apt update

## Configure sudo

Configure sudo by visudo:

    sudo visudo

Limit authentication using sudo to 3 attempts in case the password is incorrect:

    Defaults        passwd_tries=3

Add a custom error message in case of incorrect password:

    Defaults        badpass_message="<custom-error-message>"

To log all sudo commands to /var/log/sudo/<filename>:

        $ sudo mkdir /var/log/sudo
        <~~~>
        Defaults        logfile="/var/log/sudo/<filename>"
        <~~~>

To archive all sudo inputs & outputs to /var/log/sudo/:

        Defaults        log_input,log_output
        Defaults        iolog_dir="/var/log/sudo"

To require TTY:

        Defaults        requiretty

To set sudo paths to /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin:

        Defaults        secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"

<br>

# SSH

## Step 1: Installing & Configuring SSH

Install openssh-server.

    sudo apt install openssh-server

Configure SSH.

    sudo vi /etc/ssh/sshd_config

To set up SSH using Port 4242, replace below line (dont forget to remove the #, otherwise line will stay as a comment and will not take effect):

    #Port 22
with:

    Port 4242

To disable SSH login as root irregardless of authentication mechanism. Again dont forget to remove the # signal!!!!. Replace:

    #PermitRootLogin prohibit-password

with:

    PermitRootLogin no

Check SSH status via sudo service ssh status.

    sudo service ssh status

Alternatively, check SSH status via systemctl status ssh.

    sudo systemctl status ssh

## Step 2: Installing & Configuring UFW

Install ufw.

    sudo apt install ufw

Enable Firewall.

    sudo ufw enable

Allow connections using Port 4242.

    sudo ufw allow 4242

Check UFW status via sudo ufw status.

    sudo ufw status

Remove other connections (you have probably a 22 Port connection on).
First check the numbered of the rull you want to remove with:

    sudo ufw status numbered

Then remove the rule you want with:

    sudo ufw delete <number>

# User management

## Step 1: Setting Up a Strong Password Policy

**Password Age**

Configure password age policy.

    sudo vi /etc/login.defs

To set password to expire every 30 days, replace below line

    PASS_MAX_DAYS   99999

with:

    PASS_MAX_DAYS   30

To set minimum number of days between password changes to 2 days, replace below line

    PASS_MIN_DAYS   0

with:

    PASS_MIN_DAYS   2

To send user a warning message 7 days before password expiry, keep below line as is.

    PASS_WARN_AGE   7

**Password strength**

Next install the libpam-pwquality package, so that you can set password strength policies.

    apt install libpam-pwquality

Configure password strength policy. Find the the line below:

    vi /etc/pam.d/common-password
    <~~~>
    password        requisite                       pam_pwquality.so retry=3
    <~~~>

To set password minimum length to 10 characters, add below option to the above line.

    minlen=10

To require password to contain at least an uppercase character and a numeric character:

    ucredit=-1 dcredit=-1

To set a maximum of 3 consecutive identical characters:

    maxrepeat=3

To reject the password if it contains <username> in some form:

    reject_username

To set the number of changes required in the new password from the old password to 7:

    difok=7

To implement the same policy on root:

    enforce_for_root

So, in the end, the line should be similar to this:

    password        requisite                       pam_pwquality.so retry=3 minlen=10 ucredit=-1 dcredit=-1 maxrepeat=3 reject_username difok=7 enforce_for_root

*Note: You can check for man pam for more info about the package*

# Step 2: Creating a New User

Create new user.

    sudo adduser <username>

Verify whether user was successfully created.

    getent passwd <username>

Verify newly-created user's password expiry information.

    sudo chage -l <username>
    Last password change				                : <last-password-change-date>
    Password expires					                : <last-password-change-date + PASS_MAX_DAYS>
    Password inactive					                : never
    Account expires						                : never
    Minimum number of days between password change		: <PASS_MIN_DAYS>
    Maximum number of days between password change		: <PASS_MAX_DAYS>
    Number of days of warning before password expires	: <PASS_WARN_AGE>

# Step 3: Creating a New Group

Create new user42 group.

    sudo addgroup user42

Add user to user42 group.

    sudo adduser <username> user42

Check if the user was successfuly added to the group.

    getent group user42

# cron

## Setting Up a cron Job
Configure cron as root via sudo crontab -u root -e.

    sudo crontab -u root -e

To schedule a shell script to run every 10 minutes, replace below line

    # m h  dom mon dow   command

with:

    */10 * * * * sh /path/to/script

Check root's scheduled cron jobs via sudo crontab -u root -l.

    sudo crontab -u root -l

# Monitoring
You have to create a simple script called monitoring.sh It must be developed in bash. At server startup, the script will display some information (listed below) on all ter- minals every 10 minutes (take a look at wall). The banner is optional. No error must be visible. Your script must always be able to display the following information:
+ The architecture of your operating system and its kernel version.
+ The number of physical processors.
+ The number of virtual processors.
+ The current available RAM on your server and its utilization rate as a percentage.
+ The current available memory on your server and its utilization rate as a percentage.
+ The current utilization rate of your processors as a percentage.
+ The date and time of the last reboot.
+ Whether LVM is active or not.
+ The number of active connections.
+ The number of users using the server.
+ The IPv4 address of your server and its MAC (Media Access Control) address.
+ The number of commands executed with the sudo program.

Monitoring script is available in this repository.
You need to write it on store in /usr/local/bin folder

    sudo nano /usr/local/bin/monitoring.sh

## External resources

+ [https://www.vmware.com/topics/glossary/content/virtual-machine.html](https://www.vmware.com/topics/glossary/content/virtual-machine.html)
+ [https://wiki.ubuntu.com/AppArmor](https://wiki.ubuntu.com/AppArmor)
+ [https://www.tecmint.com/difference-between-apt-and-aptitude/](https://www.tecmint.com/difference-between-apt-and-aptitude/)
+ [https://www.ucl.ac.uk/isd/what-ssh-and-how-do-i-use-it](https://www.ucl.ac.uk/isd/what-ssh-and-how-do-i-use-it)