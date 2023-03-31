## 1. Create a Linux User with non-interactive shell
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

## 2. Linux File Permissions
the team has developed a new bash script xfusioncorp.sh. They have already copied the script on all required servers, however they did not make it executable on one the app server i.e App Server 1 in Stratos Datacenter.
Please give executable permissions to /tmp/xfusioncorp.sh script on App Server 1. Also make sure every user can execute it.

Sol:

check the file's current permissions
```sh
[root@stapp01 ~]# ls -ltr /tmp/xfusioncorp.sh
---------- 1 root root 40 Mar 23 03:24 /tmp/xfusioncorp.sh  
```

Add read and execute permissions to others (all users)
```sh
[root@stapp01 ~]# chmod o+rx /tmp/xfusioncorp.sh
```

## 3. Linux TimeZones Setting
During the daily standup, it was pointed out that the timezone across Nautilus Application Servers in Stratos Datacenter doesn't match with that of the local datacenter's timezone, which is America/Los Angeles

Sol:

check the time zone of the server
```sh
[root@stapp01 ~]# timedatectl | grep "Time zone"
     Time zone: UTC (UTC, +0000)
```
 set the time zone to given zone and verify it
 ```sh
[root@stapp01 ~]# timedatectl set-timezone "America/Los Angeles"

[root@stapp01 ~]# timedatectl | grep "Time zone"
    Time zone: America/Los Angeles (PDT, -0700)
 ```

## 4. Linux Services


## 5. Linux User Without Home


## 6. DNS Troubleshooting 
The system admins team of xFusionCorp Industries has noticed intermittent issues with DNS resolution in several apps . App Server 3 in Stratos Datacenter is having some DNS resolution issues, so we want to add some additional DNS nameservers on this server.
As a temporary fix we have decided to go with Google public DNS (ipv4). Please make appropriate changes on this server.

Sol:
check the name server in resolv.conf

```sh
[root@stapp03 ~]# cat /etc/resolv.conf
search stratos.xfusioncorp.com
nameserver 127.0.0.11
options ndots:0
```
Edit the resolv.conf and add google's name server wichi is 8.8.8.8

```sh
[root@stapp03 ~]# vi /etc/resolv.conf
```
check the file contents after changes
```sh
[root@stapp03 ~]# cat /etc/resolv.conf
search stratos.xfusioncorp.com
nameserver 127.0.0.11
nameserver 8.8.8.8
options ndots:0
```

## 7. Linux User Expiry
A developer mark has been assigned Nautilus project temporarily as a backup resource. As a temporary resource for this project, we need a temporary user for mark. create a user named mark on the App Server 1. Set expiry date to 2023-03-24 in Stratos Datacenter. Make sure the user is created as per standard and is in lowercase.

Sol:

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


## 8. Disable Root Login

Sol

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

## 9. Replace file
Replace all the occurences of "Sample" with "Software" in the file content.

Sol: 
```sh
#First check how many occurences are there
[root@stbkp01 /]# cat nautilus.xml | grep "Sample" | wc -l
66
[root@stbkp01 /]# cat nautilus.xml | grep "Software" | wc -l
20

#replace command
[root@stbkp01 /]# sed -i 's/Sample/Software/g' nautilus.xml

#check conentes
[root@stbkp01 /]# cat nautilus.xml | grep "Software" | wc -l
86
```
