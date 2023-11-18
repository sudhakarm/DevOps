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
A developer mark has been assigned Nautilus project temporarily as a backup resource. As a temporary resource for this project, we need a temporary user for mark. create a user named mark on the App Server 1. Set expiry date to 2023-03-24 in Stratos Datacenter. Make sure the user is created as per standard and is in lowercase.

<details>
<summary>Sol:</summary>
Create the user 'sai' first and check the status

```sh
[root@stapp01 ~]# adduser sai

[root@stapp01 ~]# chage -l sai
Last password change                                    : Jan 23, 2023
Password expires                                        : never
Password inactive                                       : never
Account expires                                         : never
Minimum number of days between password change          : 0
Maximum number of days between password change          : 99999
Number of days of warning before password expires       : 7


```

Set the expiry and check again

```sh
[root@stapp01 ~]# chage -E 2023-03-24 sai

[root@stapp01 ~]# chage -l sai
Last password change                                    : Jan 23, 2023
Password expires                                        : never
Password inactive                                       : never
Account expires                                         : Mar 24, 2023
Minimum number of days between password change          : 0
Maximum number of days between password change          : 99999
Number of days of warning before password expires       : 7
``` 

</details>

## 1.6	Linux User Files

There is a directory `/home/usersdata/` contains files and sub dir. Task is to copy files that are owned my user `ravi` to separate path `/ecommerce/` without changing directory structure.

<details>
<summary>Sol:</summary>
Search using find for files owned by user 'ravi'

```sh
 #This command finds the files owned by user ravi and copy them to ecomerce dir, with parent dir path.
 find /home/usersdata/ -type f -user ravi -exec cp --parents {} /ecommerce \;
```
</details>

## 1.7	Disable Root Login

Disable root login on the server 01
<details>
<summary>Sol:</summary>

```sh
[root@stapp01 ssh]# cat sshd_config | grep PermitRoot
#PermitRootLogin yes
# the setting of "PermitRootLogin without-password".
```
Edit and change the permission to 'no'

```sh
[root@stapp01 ssh]# vi sshd_config 
[root@stapp01 ssh]# cat sshd_config | grep PermitRoot
PermitRootLogin no
# the setting of "PermitRootLogin without-password".
```

Restart and check the status of sshd service
```sh
[root@stapp01 ssh]# systemctl restart sshd

[root@stapp01 ssh]# systemctl status sshd
● sshd.service - OpenSSH server daemon
   Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; vendor preset: enabled)
   Active: active (running) since Thu 2023-03-23 15:00:35 UTC; 16min ago
```

</details>

## 1.8	Linux Archives
Make anita.tar.gz compressed archive of /data/anita directory and move the archive to /home directory on Storage Server.

<details>
<summary>Sol:</summary>
Tar the directory and move it to `/home`
    
```sh   
tar -czvf anita.tar.gz /data/anita/
ls -l
mv anita.tar.gz /home/
```   
    
</details>

## 1.9	Linux File Permissions
The team has developed a new bash script xfusioncorp.sh. They have already copied the script on all required servers, however they did not make it executable on one the app server i.e App Server 1 in Stratos Datacenter.
Please give executable permissions to /tmp/xfusioncorp.sh script on App Server 1. Also make sure every user can execute it.

<details>
<summary>Sol:</summary>
check the files current permissions

```sh
  [root@stapp01 ~]# ls -ltr /tmp/xfusioncorp.sh
  ---------- 1 root root 40 Mar 23 03:24 /tmp/xfusioncorp.sh  
```

Add read and execute permissions to others (all users)

```sh
    [root@stapp01 ~]# chmod o+rx /tmp/xfusioncorp.sh
```
</details>

## 1.10	Linux Access Control List
Create ACL for user `ryan` should read and user `john` should not have access to the file `/etc/resolv.conf`
<details>
<summary>Sol:</summary>
Use setfacl for file and give specific permissions to each user.
    
```sh
    getfacl /etc/resolv.conf 
    setfacl -m u:john:-,u:ryan:r /etc/resolv.conf 
    getfacl /etc/resolv.conf
```
</details>

## 1.11	Linux String Substitute
 The backup server in the Stratos DC contains several templated XML files used by the Nautilus application. However, these template XML. files must be populated with valid data before they can be used. Replace all occurrences of the string 'Red' to 'Blue' on the XML file '/root/nautilus.xml' located in the backup server.
<details>
<summary>Sol:</summary>
Login to backup server and switch to root. 
Check number of occurences of word `Red` in file file `/root/nautilus.xml`

```sh
    [root@stbkp01 ~]# cat /root/nautilus.xml  |grep Red  | wc -l
    63
```

Replace the string to `Blue` and check the count
```sh
    [root@stbkp01 ~]# sed -i 's/Red/Blue/g' /root/nautilus.xml

    [root@stbkp01 ~]# cat /root/nautilus.xml  |grep Blue  | wc -l
    63
```
</details>

## 1.12	Linux Remote Copy
One of the Nautilus developers has copied confidential data on the jump host in Stratos DC. That data must be copied to one of the app servers. Because developers do not have access to app servers, they asked the system admins team to accomplish the task for them.

Copy /tmp/nautilus.txt.gpg file from jump server to App Server 3 at location /home/webdata.
<details>
<summary>Sol:</summary>
copy using scp command to app server 003

```sh
   [thor@jump_host ~]$ sudo scp /tmp/nautilus.txt.gpg  banner@stapp03:/tmp/
```
login and switch to root on app server 003

```sh
   [thor@jump_host ~]$ ssh banner@stapp03
   [thor@jump_host ~]$ sudo -i
```

move the file to required location

```sh
   [root@stapp03 ~]# mv /tmp/nautilus.txt.gpg  /home/webdata/
```
check and verify the contents of the destination

```sh
   [root@stapp03 ~]# ll /home/webdata/
   -rw-r--r-- 1 banner banner 43 Sep 12 11:02 nautilus.txt.gpg
```
</details>

## 1.13	Cron schedule deny to users
To stick with the security compliances, the Nautilus project team has decided to apply some restrictions on crontab access so that only allowed users can create/update the cron jobs. Limit crontab access to below specified users on App Server 2.

Allow crontab access to `yousuf` user and deny the same to user `ryan`.
<details>
<summary>Sol:</summary>
Login and switch to root on app 003

```sh
   thor@jump_host ~$ ssh banner@stapp003
   [banner@stapp03 ~]# sudo su
```
First check if users yousuf and ryan are there in that server

```sh
   [root@stapp03 ~]# id yousuf
   [root@stapp03 ~]# id ryan
```

Add user yousuf to allow list

```sh
   [root@stapp03 ~]# echo 'yousuf' >> /etc/cron.allow
```
Add user ryan to deny list

```sh
   [root@stapp03 ~]# echo 'ryan' >> /etc/cron.deny
```
Restart the crond service

```sh
   [root@stapp03 ~]# systemctl restart crond.service
```
Check the access

```sh
   [root@stapp03 ~]# su ryan
   ryan@stapp03 ~$ crontab -e
   #it should throw access denied
```
</details>

## 1.14	Linux Run Levels
New tools have been installed on the app server in Stratos Datacenter. Some of these tools can only be managed from the graphical user interface. Therefore, there are requirements for these app servers.

On all App servers in Stratos Datacenter change the default runlevel so that they can boot in GUI (graphical user interface) by default. Please do not try to reboot these servers
<details>
<summary>Sol:</summary>
Login to all app servers one after one. Run below commands. 

```sh
   thor@jump_host ~$ ssh tony@stapp001
   [tony@stapp01 ~]# sudo su
```

Check what is the default target
```sh
   [root@stapp01 ~]# systemctl get-default
   multi-user.target

```

Run level to graphical target as default

```sh
   [root@stapp01 ~]# systemctl set-default graphical.target
   Removed symlink /etc/systemd/system/default.target.
   Created symlink from /etc/systemd/system/default.target to /usr/lib/systemd/system/graphical.target.
```

Check the status and start graphical target service

```sh
  [root@stapp01 ~]# systemctl status graphical.traget
  ● graphical.target - Graphical Interface
     Loaded: loaded (/usr/lib/systemd/system/graphical.target; enabled; vendor preset: disabled)
     Active: inactive (dead)
     Docs: man:systemd.special(7)

  [root@stapp01 ~]#
  [root@stapp01 ~]# systemctl start graphical.target
  [root@stapp01 ~]# systemctl status graphical.target
  ● graphical.target - Graphical Interface
     Loaded: loaded (/usr/lib/systemd/system/graphical.target; enabled; vendor preset: disabled)
     Active: active since Mon 2023-09-25 12:32:09 UTC; 1s ago
     Docs: man:systemd.special(7)
  Sep 25 12:32:10 stapp01.stratos.xfusioncorp.com systemd[1]: Job graphical.target/start finished,...e
  Sep 25 15:32:10 stapp01.stratos.xfusioncorp.com systemd[1]: Reached target Graphical Interface.
  Hint: Some lines were ellipsized, use -l to show in full.

  [root@stapp01 ~]# systemctl get-default
  graphical.target
```
</details>

## 1.15	Linux TimeZones Setting
During the daily standup, it was pointed out that the timezone across Nautilus Application Servers in Stratos Datacenter doesn't match with that of the local datacenter's timezone, which is America/Blanc-Sablon.
<details>
<summary>Sol:</summary>
Login to app server 1 and switch to root 

```sh
   thor@jump_host ~$ ssh tony@stapp001
   [tony@stapp01 ~]$ sudo su
```

Check existing timezone on the server
```sh
	[root@stapp01 ~]# timedatectl
		    Local time: Sat 2023-09-23 18:21:32 UTC
	  Universal time: Sat 2023-09-23 18:21:32 UTC
			    RTC time: n/a
		     Time zone: UTC (UTC, +0000)
		   NTP enabled: n/a
	NTP synchronized: yes
	 RTC in local TZ: no
		    DST active: n/a 
```

See the syntax to find the available timezone commands
```sh
   [root@stapp01 ~]# timedatectl -h

```

Run Below command to set the time zone & verify it 
```sh
	[root@stapp01 ~]# timedatectl set-timezone America/Blanc-Sablon
	#verify the local time change, it must be AST
	[root@stapp01 ~]# timedatectl
		    Local time: Sat 2023-09-23 14:22:02 AST
	  Universal time: Sat 2023-09-23 18:22:02 UTC
			    RTC time: n/a
		     Time zone: America/Blanc-Sablon (AST, -0400) #<<< Timezone changed
		   NTP enabled: n/a
	NTP synchronized: yes
	 RTC in local TZ: no
	      DST active: n/a
```
</details>

## 1.16	Linux NTP Setup
The system admin team of xFusionCorp Industries has noticed an issue with some servers in Stratos Datacenter where some of the servers are not in sync w.r.t time. Because of this, several application functionalities have been impacted. To fix this issue the team has started using common/standard NTP servers. They are finished with most of the servers except App Server 1. Therefore, perform the following tasks on this server:

Install and configure NTP server on App Server 1.

Add NTP server 1.sg.pool.ntp.org in NTP configuration on App Server 1.

Please do not try to start/restart/stop ntp service, as we already have a restart for this service scheduled for tonight and we don't want these changes to be applied right now.
<details>
<summary>Sol:</summary>
Login to app server 1 and switch to root 

```sh
   thor@jump_host ~$ ssh tony@stapp001
   [tony@stapp01 ~]$ sudo su
```

Check NTP is installed , if not then install on the server 

```sh
	[root@stapp01 ~]# rpm -qa |grep ntp
	[root@stapp01 ~]# 
	[root@stapp01 ~]# yum install -y ntp
	Loaded plugins: fastestmirror, ovl
	Determining fastest mirrors
	 * base: ftpmirror.your.org
	 * extras: bay.uchicago.edu
	 * updates: ftpmirror.your.org
	base                                                                       | 3.6 kB  00:00:00    
	extras                                                                     | 2.9 kB  00:00:00    
	updates                                                                    | 2.9 kB  00:00:00    
	(1/4): base/7/x86_64/group_gz                                              | 153 kB  00:00:00    
	(2/4): extras/7/x86_64/primary_db                                          | 242 kB  00:00:00    
	(3/4): base/7/x86_64/primary_db                                            | 6.1 MB  00:00:00    
	(4/4): updates/7/x86_64/primary_db                                         | 8.8 MB  00:00:00    

	Resolving Dependencies

	--> Running transaction check
	---> Package ntp.x86_64 0:4.2.6p5-29.el7.centos.2 will be installed
	--> Processing Dependency: ntpdate = 4.2.6p5-29.el7.centos.2 for package: ntp-4.2.6p5-29.el7.centos.2.x86_64
	--> Processing Dependency: libopts.so.25()(64bit) for package: ntp-4.2.6p5-29.el7.centos.2.x86_64
	--> Running transaction check
	---> Package autogen-libopts.x86_64 0:5.18-5.el7 will be installed
	---> Package ntpdate.x86_64 0:4.2.6p5-29.el7.centos.2 will be installed
	--> Finished Dependency Resolution
	 
	Dependencies Resolved

	===============================================================================================
	Package                  Arch            Version                             Repository     Size
	==================================================================================================

	Installing:
	 ntp                      x86_64          4.2.6p5-29.el7.centos.2             base          549 k
	Installing for dependencies:
	 autogen-libopts          x86_64          5.18-5.el7                          base           66 k
	 ntpdate                  x86_64          4.2.6p5-29.el7.centos.2             base           87 k

	Transaction Summary
	==================================================================================================
	Install  1 Package (+2 Dependent packages)
	Total download size: 701 k
	Installed size: 1.6 M
	Downloading packages:
	(1/3): autogen-libopts-5.18-5.el7.x86_64.rpm                               |  66 kB  00:00:00    
	(2/3): ntpdate-4.2.6p5-29.el7.centos.2.x86_64.rpm                          |  87 kB  00:00:00    
	(3/3): ntp-4.2.6p5-29.el7.centos.2.x86_64.rpm                              | 549 kB  00:00:00    
	--------------------------------------------------------------------------------------------------
	Total                                                             1.2 MB/s | 701 kB  00:00:00    

	Running transaction check
	Running transaction test
	Transaction test succeeded
	Running transaction
	  Installing : autogen-libopts-5.18-5.el7.x86_64                                              1/3
	  Installing : ntpdate-4.2.6p5-29.el7.centos.2.x86_64                                         2/3
	  Installing : ntp-4.2.6p5-29.el7.centos.2.x86_64                                             3/3
	  Verifying  : ntpdate-4.2.6p5-29.el7.centos.2.x86_64                                         1/3
	  Verifying  : ntp-4.2.6p5-29.el7.centos.2.x86_64                                             2/3
	  Verifying  : autogen-libopts-5.18-5.el7.x86_64                                              3/3
	 Installed:
	  ntp.x86_64 0:4.2.6p5-29.el7.centos.2                                                           
	 Dependency Installed:
	  autogen-libopts.x86_64 0:5.18-5.el7           ntpdate.x86_64 0:4.2.6p5-29.el7.centos.2         
	 Complete!
	 
```

Add NTP server in configuration file in the end as per task `1.sg.pool.ntp.org`
```sh
	[root@stapp01 ~]# vi /etc/ntp.conf
	[root@stapp01 ~]#
	[root@stapp01 ~]# cat /etc/ntp.conf |grep sg.pool
	 server 1.sg.pool.ntp.org
```
Check NTP daemon status  
```sh
	[root@stapp01 ~]# ntpstat
	Unable to talk to NTP daemon. Is it running?

	[root@stapp01 ~]# systemctl status ntpd
	● ntpd.service - Network Time Service
	   Loaded: loaded (/usr/lib/systemd/system/ntpd.service; disabled; vendor preset: disabled)
	   Active: inactive (dead)
```

As per task description a nightly cron job will start the service. So no need to restart the service. Just enable that.
```sh
	[root@stapp01 ~]# systemctl enable ntpd
	Created symlink from /etc/systemd/system/multi-user.target.wants/ntpd.service to /usr/lib/systemd/system/ntpd.service.
```
</details>

## 1.17	Linux Firewalld Rules
The Nautilus system admins team recently deployed a web UI application for their backup utility running on the Nautilus backup server in Stratos Datacenter. The application is running on port 5004. They have firewalld installed on that server. The requirements that have come up include the following:

<details>
<summary>Sol:</summary>
Login to backup and switch to root 

```sh
   thor@jump_host ~$ ssh clint@stbkp01
   [clint@stbkp01 ~]$ sudo su
```

List existing rules
```sh
	[root@stbkp01 ~]# firewall-cmd --zone=public --list-all
	public
	  target: default
	  icmp-block-inversion: no
	  interfaces:
	  sources:
	  services: dhcpv6-client ssh
	  ports:
	  protocols:
	  masquerade: no
	  forward-ports:
	  source-ports:
	  icmp-blocks:
	  rich rules:
```

Open all incoming connection on 5004/tcp port. Zone should be public.

```sh
	[root@stbkp01 ~]# firewall-cmd --permanent --zone=public --add-port=5004/tcp
  success
	
	#reload the firewall for changes to affect
	[root@stbkp01 ~]# firewall-cmd --reload
  success
```

Check the list again and see ports

```sh
	[root@stbkp01 ~]# firewall-cmd --list-all
	public
	  target: default
	  icmp-block-inversion: no
	  interfaces:
	  sources:
	  services: dhcpv6-client ssh
	  ports: 5004/tcp
	  protocols:
	  masquerade: no
	  forward-ports:
	  source-ports:
	  icmp-blocks:
	  rich rules:
  
  # see ports
	[root@stbkp01 ~]# firewall-cmd --list-ports
  5004/tcp

```

</details>

## 1.18	Linux Resource Limits
On our Storage server in Stratos Datacenter we are having some issues where nfsuser user is holding hundred of processes, which is degrading the performance of the server. Therefore, we have a requirement to limit its maximum processes. Please set its maximum process limits as below:

a. soft limit = 1026
b. hard_limit = 2025
<details>
<summary>Sol:</summary>
Login to storage server and switch to root 

```sh
   thor@jump_host ~$ ssh natasha@ststor01
   [natasha@ststor01 ~]$ sudo su
```

Edit the limits configuration file to add soft and hard limits for nproc
```sh
[root@ststor01 natasha]# vi /etc/security/limits.conf 

#add below lines
	nfsuser          soft    nproc           1026
	nfsuser          hard    nproc           2025
```

see changes

```sh
	[root@ststor01 natasha]# cat /etc/security/limits.conf | grep nproc | grep -v ^#
	nfsuser          soft    nproc           1026
	nfsuser          hard    nproc           2025
```
</details>

## 1.19	Selinux Installation
Install the required packages of SElinux on App server 1 in Stratos Datacenter and disable it permanently for now; it will be enabled after making some required configuration changes on this host. Don't worry about rebooting the server as there is already a reboot scheduled for tonight's maintenance window. Also ignore the status of SElinux command line right now; the final status after reboot should be disabled
<details>
<summary>Sol:</summary>
Login to app server 1 and switch to root

```sh
   thor@jump_host ~$ ssh tony@stapp001
   [tony@stapp01 ~]# sudo su
```
Install selinux ( it takes 5-10 mins)

```sh
   [root@stapp01 tony]#  yum -y install selinux*
```

Check the existing  SElinux  status
```sh
  [root@stapp03 ~]# sestatus
   SELinux status:                 disabled
```

Check in the config as well
```sh
	[root@stapp01 tony]# cat /etc/selinux/config | grep SELINUX
	# SELINUX= can take one of these three values:
	SELINUX=enforcing
	# SELINUXTYPE= can take one of these three values:
	SELINUXTYPE=targeted
```

Since the status shows `SELINUX=enforcing` change it to disabled and then see the status.

```sh
	#edit config and change status to disabled
	[root@stapp01 tony]# vi /etc/selinux/config
	
	#check after the change
	[root@stapp01 tony]# cat /etc/selinux/config | grep SELINUX
	# SELINUX= can take one of these three values:
	SELINUX=disabled
	# SELINUXTYPE= can take one of these three values:
	SELINUXTYPE=targeted
	
	#check status
	[root@stapp01 tony]# sestatus
	SELinux status:                 disabled
```
</details>

## 1.20	Linux User Expiry
 A developer mark has been assigned Nautilus project temporarily as a backup resource. As a temporary resource for this project, we need a temporary user for mark. It’s a good idea to create a user with a set expiration date so that the user won't be able to access servers beyond that point.

Therefore, create a user named mark on the App Server 1. Set expiry date to 2023-11-15 in Stratos Datacenter. Make sure the user is created as per standard and is in lowercase.
<details>
<summary>Sol:</summary>
Login to app server1 and switch to root

```sh
   thor@jump_host ~$ ssh tony@stapp001
   [tony@stapp01 ~]$ sudo su
```
Check if the user exist on server
```sh
	[root@stapp01 ~]# id  mark
	id: mark: no such user
```

create user 
```sh
	[root@stapp01 ~]# adduser mark

	#check user again
	[root@stapp01 ~]# id  mark
	uid=1002(mark) gid=1002(mark) groups=1002(mark)
```

Validate the expirt of user
```sh
	[root@stapp01 ~]# chage -l mark
	Last password change                                    : Nov 18, 2023
	Password expires                                        : never
	Password inactive                                       : never
	Account expires                                         : never
	Minimum number of days between password change          : 0
	Maximum number of days between password change          : 99999
	Number of days of warning before password expires       : 7
```

Run below command to set the expiry
```sh
chage -E 2023-12-15 mark

#check again the expiry
	[root@stapp01 ~]# chage -l mark
	Last password change                                    : Nov 18, 2023
	Password expires                                        : never
	Password inactive                                       : never
	Account expires                                         : Dec 15, 2023
	Minimum number of days between password change          : 0
	Maximum number of days between password change          : 99999
	Number of days of warning before password expires       : 7

```
</details>



# Linux Level 2

## 2.1	Create a Cron Job
The Nautilus system admins team has prepared scripts to automate several day-to-day tasks. They want them to be deployed on all app servers in Stratos DC on a set schedule. Before that they need to test similar functionality with a sample cron job. Therefore, perform the steps below:

a. Install cronie package on all Nautilus app servers and start crond service.
b. Add a cron */5 * * * * echo hello > /tmp/cron_text for root user.
<details>
<summary>Sol:</summary>
Login to all 3 app servers and switch to root

```sh
   thor@jump_host ~$ ssh tony@stapp001
   [tony@stapp01 ~]$ sudo su
```

Install cronie on stapp01, similarly do on all 3 servers
```sh
	[root@stapp01 ~]# yum install -y cronie
```

Start the cron service and check status
```sh
	[root@stapp01 ~]# systemctl start crond.service
	[root@stapp01 ~]# systemctl status crond.service
	● crond.service - Command Scheduler
	   Loaded: loaded (/usr/lib/systemd/system/crond.service; enabled; vendor preset: enabled)
	   Active: active (running) since Sat 2023-11-18 05:54:38 UTC; 4min 22s ago
	 Main PID: 427 (crond)
		Tasks: 1 (limit: 1340692)
	   Memory: 1.1M
	   CGroup: /docker/9a188d9e699c345715240502a95d9c7a7a2841e236cd5abb59f6a01ba89f0b46/system.slice/crond.service
			   └─427 /usr/sbin/crond -n

	Nov 18 05:54:38 stapp01.stratos.xfusioncorp.com systemd[1]: Started Command Scheduler.
	Nov 18 05:54:38 stapp01.stratos.xfusioncorp.com systemd[427]: crond.service: Executing: /u
	sr/sbin/crond -n
	Nov 18 05:54:38 stapp01.stratos.xfusioncorp.com crond[427]: (CRON) STARTUP (1.5.2)
	Nov 18 05:54:38 stapp01.stratos.xfusioncorp.com crond[427]: (CRON) INFO (Syslog will be used instead of sendmail.)
	Nov 18 05:54:38 stapp01.stratos.xfusioncorp.com crond[427]: (CRON) INFO (RANDOM_DELAY will be scaled with factor 6
	8% if used.)
	Nov 18 05:54:38 stapp01.stratos.xfusioncorp.com crond[427]: (CRON) INFO (running with inotify support)
	Nov 18 05:58:55 stapp01.stratos.xfusioncorp.com systemd[1]: crond.service: Trying to enque
	ue job crond.service/start/replace
	Nov 18 05:58:55 stapp01.stratos.xfusioncorp.com systemd[1]: crond.service: Installed new j
	ob crond.service/start as 57
	Nov 18 05:58:55 stapp01.stratos.xfusioncorp.com systemd[1]: crond.service: Enqueued job cr
	ond.service/start as 57
	Nov 18 05:58:55 stapp01.stratos.xfusioncorp.com systemd[1]: crond.service: Job crond.servi
	ce/start finished, result=done
```

Edit the crontab and add the rule.
```sh
	[root@stapp01 ~]# crontab -e
	no crontab for root - using an empty one
	crontab: installing new crontab

	[root@stapp01 ~]# crontab -l
	*/5 * * * * echo hello > /tmp/cron_text

```

Check if that cron is working.
```sh
	[root@stapp01 ~]# cat /tmp/cron_text
	hello

  # also check on other servers the output os service status shows the cronjob ran `CMD (echo hello > /tmp/cron_text)`
  [root@stapp02 steve]# cat /tmp/cron_text 
	hello
	[root@stapp02 steve]# systemctl status crond
	● crond.service - Command Scheduler
	   Loaded: loaded (/usr/lib/systemd/system/crond.service; enabled; vendor preset: enabled)
	   Active: active (running) since Sat 2023-11-18 05:54:35 UTC; 16min ago
	 Main PID: 520 (crond)
		Tasks: 2 (limit: 1340692)
	   Memory: 6.6M
	   CGroup: /docker/2b4b7d1e839c0e6609e8888da3cfe6dc5cb48535e5036953dabbd6e2a0d31c04/system.slice/crond.service
			   ├─520 /usr/sbin/crond -n
			   └─639 /usr/sbin/anacron -s

	Nov 18 06:01:01 stapp02.stratos.xfusioncorp.com CROND[623]: (root) CMD (run-parts /etc/cron.hourly)
	Nov 18 06:01:01 stapp02.stratos.xfusioncorp.com anacron[639]: Anacron started on 2023-11-1
	8
	Nov 18 06:01:01 stapp02.stratos.xfusioncorp.com anacron[639]: Will run job `cron.daily' in
	 11 min.
	Nov 18 06:01:01 stapp02.stratos.xfusioncorp.com anacron[639]: Will run job `cron.weekly' i
	n 31 min.
	Nov 18 06:01:01 stapp02.stratos.xfusioncorp.com anacron[639]: Will run job `cron.monthly' 
	in 51 min.
	Nov 18 06:01:01 stapp02.stratos.xfusioncorp.com anacron[639]: Jobs will be executed sequen
	tially
	Nov 18 06:05:01 stapp02.stratos.xfusioncorp.com crond[762]: pam_systemd(crond:session): Fa
	iled to create session: Unit systemd-logind.service is masked.
	Nov 18 06:05:01 stapp02.stratos.xfusioncorp.com CROND[769]: (root) CMD (echo hello > /tmp/cron_text)
	Nov 18 06:10:01 stapp02.stratos.xfusioncorp.com crond[771]: pam_systemd(crond:session): Fa
	iled to create session: Unit systemd-logind.service is masked.
	Nov 18 06:10:01 stapp02.stratos.xfusioncorp.com CROND[780]: (root) CMD (echo hello > /tmp/cron_text)

```
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
The Nautilus DevOps team is ready to launch a new application, which they will deploy on app servers in Stratos Datacenter. They are expecting significant traffic/usage of `squid` on app servers after that. This will generate massive logs, creating huge log files. To utilise the storage efficiently, they need to compress the log files and need to rotate old logs. Check the requirements shared below:

a. In all app servers install `squid` package.
b. Using `logrotate` configure `squid` logs rotation to monthly and keep only 3 rotated logs.
(If by default log rotation is set, then please update configuration as needed)
<details>
<summary>Sol:</summary>
    
Install squid package

```sh
[root@stapp01 ~]# yum install squid -y
```

Navigate to logrotate folder and check existing folder

```sh
[root@stapp01 ~]# ls -l /etc/logrotate.d/
total 20
-rw-r--r-- 1 root root 130 Feb  8  2023 btmp
-rw-r--r-- 1 root root  88 Apr 12  2021 dnf
-rw-r--r-- 1 root root 435 Dec 20  2022 squid
-rw-r--r-- 1 root root  88 Aug  8  2022 subscription-manager
-rw-r--r-- 1 root root 145 Feb 19  2018 wtmp
```

Check contents of squid log rotation

```sh
[root@stapp01 ~]# cat /etc/logrotate.d/squid
/var/log/squid/*.log {
    weekly
    rotate 5
    compress
    notifempty
    missingok
    nocreate
    sharedscripts
    postrotate
      # Asks squid to reopen its logs. (logfile_rotate 0 is set in squid.conf)
      # errors redirected to make it silent if squid is not running
      /usr/sbin/squid -k rotate 2>/dev/null
      # Wait a little to allow Squid to catch up before the logs is compressed
      sleep 1
    endscript
}
```

Edit and change the time to monthly and rotation to 3

```sh
[root@stapp01 ~]# vi /etc/logrotate.d/squid
# After change
[root@stapp01 ~]# cat /etc/logrotate.d/squid
/var/log/squid/*.log {
    monthly
    rotate 3
    compress
    notifempty
    missingok
    nocreate
    sharedscripts
    postrotate
      # Asks squid to reopen its logs. (logfile_rotate 0 is set in squid.conf)
      # errors redirected to make it silent if squid is not running
      /usr/sbin/squid -k rotate 2>/dev/null
      # Wait a little to allow Squid to catch up before the logs is compressed
      sleep 1
    endscript
}
```

Restart the squid service and check status

```sh
[root@stapp01 ~]# systemctl start squid
[root@stapp01 ~]# systemctl status squid
● squid.service - Squid caching proxy
   Loaded: loaded (/usr/lib/systemd/system/squid.service; disabled; vendor preset: disabled)
   Active: active (running) since Wed 2023-09-13 13:04:16 UTC; 11s ago
     Docs: man:squid(8)
```
</details>


## 2.24	Application Security
We have a backup management application UI hosted on Nautilus's backup server in Stratos DC. That backup management application code is deployed under Apache on the backup server itself, and Nginx is running as a reverse proxy on the same server. Apache and Nginx ports are 8085 and 8091, respectively. We have iptables firewall installed on this server. Make the appropriate changes to fulfill the requirements mentioned below:

We want to open all incoming connections to Nginx's port (8091) and block all incoming connections to Apache's port (8085). Also make sure rules are permanent.

<details>
<summary>Sol:</summary>
Check if iptables service is running

```sh
systemctl status iptables
systemctl start iptables
```
Now create deny and allow rules in IP tables and save permanently
```sh
[root@stbkp01 ~]# iptables -A INPUT -p tcp --dport 8085 -m conntrack --ctstate NEW -j REJECT
[root@stbkp01 ~]# iptables -A INPUT -p tcp --dport 8091 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
[root@stbkp01 ~]# service iptables save
iptables: Saving firewall rules to /etc/sysconfig/iptables:[  OK  ]
```

Check if rules saved as per config
```sh
[root@stbkp01 ~]# iptables-save | grep 80
:INPUT ACCEPT [126:8808]
-A INPUT -p tcp -m tcp --dport 8085 -m conntrack --ctstate NEW -j REJECT --reject-with icmp-port-unreachable
-A INPUT -p tcp -m tcp --dport 8091 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
```
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
