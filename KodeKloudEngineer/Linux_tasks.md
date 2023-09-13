# KodeKloud Engineer - Linux Tasks - 2023

## 1.1. Create a user
a. Create a user named kareem on the App server 3 in Stratos Datacenter.
b. Set UID to 1190 and its home directory to /var/www/kareem.

Sol:
Login to the app server 3 and switch to root
```
thor@jump_host ~$ ssh banner@stapp03
```
Add user 
```
[root@stapp03 ~]# useradd -u 1190 kareem
[root@stapp03 ~]# id kareem
uid=1190(kareem) gid=1190(kareem) groups=1190(kareem)
```

Check if user created or not
```
[root@stapp03 ~]# cat /etc/passwd | grep kareem
kareem:x:1190:1190::/var/www/kareem:/bin/bash
```

## 1.2. Create a group
There are specific access levels for users defined by the xFusionCorp Industries system admin team. Rather than providing access levels to every individual user, the team has decided to create groups with required access levels and add users to that groups as needed. See the following requirements:

a. Create a group named nautilus_developers in all App servers in Stratos Datacenter.

### Sol:
Login to app server 1 and sudo
```
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
```
[root@stapp01 ~]# groupadd nautilus_developers
[root@stapp01 ~]# id rajesh
id: 'rajesh': no such user
[root@stapp01 ~]# useradd -G nautilus_developers rajesh

```

Verify the user's group
```
[root@stapp01 ~]# id rajesh
uid=1002(rajesh) gid=1003(rajesh) groups=1003(rajesh),1002(nautilus_developers)
[root@stapp01 ~]# cat /etc/passwd | grep raj
rajesh:x:1002:1003::/home/rajesh:/bin/bash
```

## 1.3. Create a Linux User with non-interactive shell
Create a Linux User 'sam' with a non-interactive shell The System Admin Team of XfusionCorp Industries has installed a backup agent tool on all app servers. As per the tool's requirements, they need to create a user with a non-interactive shell. 

Sol:

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

## 1.4. Linux User Without Home
The system admins team of xFusionCorp Industries has set up a new tool on all app servers, as they have a requirement to create a service user account that will be used by that tool. They are finished with all apps except for App Server 1 in Stratos Datacenter.

Create a user named javed in App Server 1 without a home directory

Sol:
At first login on app server given in task & Switch to  root user
Check user javed is there, if not then create
```
[root@stapp01 ~]# id javed
id: mohammed: no such user

[root@stapp01 ~]# cat /etc/passwd |grep javed

```

create a user javed with below commands ( check user name in your task)     
```
[root@stapp01 ~]# useradd -M javed
[root@stapp01 ~]#
```

Validate the task by listing the file exist in  Home directory  
```
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