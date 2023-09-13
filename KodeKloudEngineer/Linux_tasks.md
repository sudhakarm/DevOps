# KodeKloud Engineer - Linux Tasks - 2023

## 1.1. Create a user
a. Create a user named kareem on the App server 3 in Stratos Datacenter.
b. Set UID to 1190 and its home directory to /var/www/kareem.
<details>
<summary>Sol:</summary>
Login to the app server 3 and switch to root
    
```sh
thor@jump_host ~$ ssh banner@stapp03
```
Add user 

```sh
[root@stapp03 ~]# useradd -u 1190 kareem
[root@stapp03 ~]# id kareem
uid=1190(kareem) gid=1190(kareem) groups=1190(kareem)
```

Check if user created or not

```sh
[root@stapp03 ~]# cat /etc/passwd | grep kareem
kareem:x:1190:1190::/var/www/kareem:/bin/bash
```
</details>

## 1.2. Create a group
There are specific access levels for users defined by the xFusionCorp Industries system admin team. Rather than providing access levels to every individual user, the team has decided to create groups with required access levels and add users to that groups as needed. See the following requirements:

a. Create a group named nautilus_developers in all App servers in Stratos Datacenter.

<details>
<summary>Sol:</summary>

Login to app server 1 and sudo
```sh
thor@jump_host ~$ ssh tony@stapp01
The authenticity of host 'stapp01 (172.16.238.10)' can't be established.
ECDSA key fingerprint is SHA256:JhOqund8gadKYbCYr6cmFmQJRR1efsNB7ecz1qytQog.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'stapp01,172.16.238.10' (ECDSA) to the list of known hosts.
tony@stapp01's password: 
[tony@stapp01 ~]$ sudo -i

We trust you have received the usual lecture from the local System
Administrator. It usually boils down to these three things:

    #1) Respect the privacy of others.
    #2) Think before you type.
    #3) With great power comes great responsibility.

[sudo] password for tony:
```

create a group . Also create user, add them to group using -G at the same time
```sh
[root@stapp01 ~]# groupadd nautilus_developers
[root@stapp01 ~]# id rajesh
id: 'rajesh': no such user
[root@stapp01 ~]# useradd -G nautilus_developers rajesh

```

Verify the user's group
```sh
[root@stapp01 ~]# id rajesh
uid=1002(rajesh) gid=1003(rajesh) groups=1003(rajesh),1002(nautilus_developers)
[root@stapp01 ~]# cat /etc/passwd | grep raj
rajesh:x:1002:1003::/home/rajesh:/bin/bash
```
</details>

## 1.3. Create a Linux User with non-interactive shell
Create a Linux User 'sam' with a non-interactive shell The System Admin Team of XfusionCorp Industries has installed a backup agent tool on all app servers. As per the tool's requirements, they need to create a user with a non-interactive shell. 

<details>
<summary>Sol:</summary>

Check if the user exist on system.
```sh
[root@stapp01]# id sam
id: sam: no such user
```
If not, create the user
```sh
[root@stapp01 ~]# adduser sam  -s /sbin/nologin
```
Check the user now
```sh
[root@stapp01 ~]# id sam
uid=1002(sam) gid=1002(sam) groups=1002(sam)
```
validate the user created as nologin
```sh
[root@stapp02 ~]# cat /etc/passwd | grep sam
sam:x:1002:1002::/home/sam:/sbin/nologin
```
</details>

## 1.4. Linux User Without Home
The system admins team of xFusionCorp Industries has set up a new tool on all app servers, as they have a requirement to create a service user account that will be used by that tool. They are finished with all apps except for App Server 1 in Stratos Datacenter.

Create a user named javed in App Server 1 without a home directory

<details>
<summary>Sol:</summary>
At first login on app server given in task & Switch to  root user
Check user javed is there, if not then create
```sh
[root@stapp01 ~]# id javed
id: mohammed: no such user

[root@stapp01 ~]# cat /etc/passwd |grep javed

```

create a user javed with below commands ( check user name in your task)     
```sh
[root@stapp01 ~]# useradd -M javed
[root@stapp01 ~]#
```

Validate the task by listing the file exist in  Home directory  
```sh
[root@stapp01 ~]# id javed
uid=1002(javed) gid=1002(javed) groups=1002(javed)
[root@stapp01 ~]#

[root@stapp01 ~]# cat /etc/passwd |grep javed
javed:x:1002:1002::/home/javed:/bin/bash
[root@stapp01 ~]#

[root@stapp01 ~]# ll /home
total 8
drwx------ 1 ansible ansible 4096 Oct 15  2019 ansible
drwx------ 1 tony    tony    4096 Jan 25  2020 tony
[root@stapp01 ~]#
```
</details>

## 1.5	Linux User Expiry
<details>
<summary>Sol:</summary>

</details>

## 1.6	Linux User Files
<details>
<summary>Sol:</summary>

</details>

## 1.7	Disable Root Login
<details>
<summary>Sol:</summary>

</details>

## 1.8	Linux Archives
<details>
<summary>Sol:</summary>

</details>

## 1.9	Linux File Permissions
<details>
<summary>Sol:</summary>

</details>

## 1.10	Linux Access Control List
<details>
<summary>Sol:</summary>

</details>

## 1.11	Linux String Substitute
<details>
<summary>Sol:</summary>

</details>

## 1.12	Linux Remote Copy
<details>
<summary>Sol:</summary>

</details>

## 1.13	Cron schedule deny to users
<details>
<summary>Sol:</summary>

</details>

## 1.14	Linux Run Levels
<details>
<summary>Sol:</summary>

</details>

## 1.15	Linux TimeZones Setting
<details>
<summary>Sol:</summary>

</details>

## 1.16	Linux NTP Setup
<details>
<summary>Sol:</summary>

</details>

## 1.17	Linux Firewalld Rules
<details>
<summary>Sol:</summary>

</details>

## 1.18	Linux Resource Limits
<details>
<summary>Sol:</summary>

</details>

## 1.19	Selinux Installation
<details>
<summary>Sol:</summary>

</details>

## 1.20	Linux User Expiry
<details>
<summary>Sol:</summary>

</details>



# Linux Level 2

## 2.1	Create a Cron Job
<details>
<summary>Sol:</summary>

</details>

## 2.2	Linux Banner
<details>
<summary>Sol:</summary>

</details>

## 2.3	Linux Collaborative Directories
<details>
<summary>Sol:</summary>

</details>

## 2.4	Linux String Substitute (sed)
<details>
<summary>Sol:</summary>

</details>

## 2.5	Linux SSH Authentication
<details>
<summary>Sol:</summary>

</details>

## 2.6	Linux Find Command
<details>
<summary>Sol:</summary>

</details>

## 2.7	Linux Install a package
<details>
<summary>Sol:</summary>

</details>

## 2.8	Linux Install Ansible
<details>
<summary>Sol:</summary>

</details>

## 2.9	Linux Configure Local Yum repos
<details>
<summary>Sol:</summary>

</details>

## 2.10	Linux Services
<details>
<summary>Sol:</summary>

</details>

## 2.11	Linux Configure sudo
<details>
<summary>Sol:</summary>

</details>

## 2.12	DNS Troubleshooting
<details>
<summary>Sol:</summary>

</details>

## 2.13	Linux Firewalld Setup
<details>
<summary>Sol:</summary>

</details>

## 2.14	Linux Postfix Mail Server
<details>
<summary>Sol:</summary>

</details>

## 2.15	Linux Postfix Troubleshooting
<details>
<summary>Sol:</summary>

</details>

## 2.16	Linux Install and
<details>
<summary>Sol:</summary>

</details>

## 2.17	Linux Haproxy LBR Troubleshooting
<details>
<summary>Sol:</summary>

</details>

## 2.18	MariaDB Troubleshooting
<details>
<summary>Sol:</summary>

</details>

## 2.19	Linux Bash Scripts
<details>
<summary>Sol:</summary>

</details>

## 2.20	Add Response Headers in Apache
<details>
<summary>Sol:</summary>

</details>

## 2.21	Apache Troubleshooting
<details>
<summary>Sol:</summary>

</details>

## 2.22	Linux GPG Encryption
<details>
<summary>Sol:</summary>

</details>

## 2.23	Linux LogRotate
<details>
<summary>Sol:</summary>

</details>

## 2.24	Application Security
<details>
<summary>Sol:</summary>

</details>



# Linux Level 3

## 3.1	Apache Redirects
<details>
<summary>Sol:</summary>

</details>

## 3.2	Install And Configure SFTP
<details>
<summary>Sol:</summary>

</details>

## 3.3	Install and Configure Tomcat Server
<details>
<summary>Sol:</summary>

</details>

## 3.4	Linux Network Services
<details>
<summary>Sol:</summary>

</details>

## 3.5	IPtables Installation And Configuration
<details>
<summary>Sol:</summary>

</details>

## 3.6	Linux Nginx as Reverse Proxy
<details>
<summary>Sol:</summary>

</details>

## 3.7	Configure protected directories in Apache
<details>
<summary>Sol:</summary>

</details>

## 3.8	Linux Process Troubleshooting
<details>
<summary>Sol:</summary>

</details>

## 3.9	PAM Authentication For Apache
<details>
<summary>Sol:</summary>

</details>

## 3.10	Setup SSL for Nginx
<details>
<summary>Sol:</summary>

</details>



# Linux Level 4

## 4.1	Install and Configure Nginx as an LBR
<details>
<summary>Sol:</summary>

</details>

## 4.2	LEMP Troubleshooting
<details>
<summary>Sol:</summary>

</details>

## 4.3	Install and Configure PostgreSQL
<details>
<summary>Sol:</summary>

</details>

## 4.4	Bash scripts if/else statements
<details>
<summary>Sol:</summary>

</details>

## 4.5	Configure LAMP server
<details>
<summary>Sol:</summary>

</details>

## 4.6	Install and Configure DB Server
<details>
<summary>Sol:</summary>

</details>

## 4.7	Install and Configure Web Application
<details>
<summary>Sol:</summary>

</details>

## 4.8	Install and Configure PHP-FPM
<details>
<summary>Sol:</summary>

</details>

## 4.9	Configure Nginx + PHP-FPM Using Unix Sock
<details>
<summary>Sol:</summary>

</details>
