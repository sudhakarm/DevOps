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

## 10. Banner message
copy existing banner message to the server.

Sol:
Find out if scp is working on the target server, otherwise install it with `yum install openssl-clients`

copy the file using scp to temp location
```sh
thor@jump_host ~$ scp -r /home/thor/nautilus_banner peter@stdb01:/tmp/
peter@stdb01's password: 
nautilus_banner                                                                                        100% 2530     6.5MB/s   00:00    

```

Login to the target server and move the file from temp to /etc/motd/ directory.
```sh
thor@jump_host ~$ ssh peter@stdb01
peter@stdb01's password: 
Last login: Mon Apr  3 10:27:15 2023 from jump_host.linux-banner-v2_db_net
[peter@stdb01 ~]$ sudo -i
[sudo] password for peter: 
           
[root@stdb01 ~]# mv /tmp/nautilus_banner /etc/motd 
mv: overwrite ‘/etc/motd’? y
```

After copy, logout from the server and login again to see the banner
```sh
ssh peter@stdb01
#### Shows the banner message #####
```
## 11. Linux User Files
there is a directory `/home/usersdata/` contains files and sub dir. Task is to copy files that are owned my user `ravi` to separate path `/ecommerce/` without changing directory structure.

sol:

```sh
 #This command finds the files owned by user ravi and copy them to ecomerce dir, with parent dir path.
 find /home/usersdata/ -type f -user ravi -exec cp --parents {} /ecommerce \;

```
## 12. Linux SSH Authentication
Set up a password-less authentication from user thor on jump host to all app servers through their respective sudo users.

Sol: 
First generate an rsa public key from jump server as thor. using `ssh-keygen`. 
Give passphrase as empty for now.
```sh
thor@jump_host ~$ ssh-keygen -t rsa

Generating public/private rsa key pair.
Enter file in which to save the key (/home/thor/.ssh/id_rsa):
Created directory '/home/thor/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/thor/.ssh/id_rsa.
Your public key has been saved in /home/thor/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:C25X9Nv4Vgiw2U7cbxFQxLXsFgTPgtH3G/Hf+DspASD thor@jump_host.stratos.xfusioncorp.com
The key's randomart image is:
+---[RSA 2048]----+
|          .o+*+*+  |
|        .  +=O . |
|      .  ++ o.X  |
|       *.oo+E +o=.|
|      o S..o o+oo|
|       . +.o+.=. |
|        o oo.+  o|
|           .o. o.|
|           .. ...|
+----[SHA256]-----+

thor@jump_host ~$
```

Now copy this pub key to the application server using `ssh-copy-id`, in the process you need to give password of user in that server. In this case you have to give password of the user `tony` on app server `stapp01`
```sh

thor@jump_host ~$ ssh-copy-id  tony@stapp01

/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/thor/.ssh/id_rsa.pub"
The authenticity of host 'stapp01 (172.16.238.10)' can't be established.
ECDSA key fingerprint is SHA256:xOVel/2X5Nx5p4t62XYbazZrYXBcpWM/z32+OL2GaMsX.
ECDSA key fingerprint is MD5:a4:1f:34:cc:9e:2c:da:c0:f3:c9:cc:e3:c2:3c:12:51.

Are you sure you want to continue connecting (yes/no)? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys

tony@stapp01's password:

 Number of key(s) added: 1
 Now try logging into the machine, with:   "ssh 'tony@stapp01'"
and check to make sure that only the key(s) you wanted were added.
 thor@jump_host /$
```

Check after copying rsa. Check by logging in to server. It will not ask password.

```sh
thor@jump_host ~$ ssh tony@stapp01
tony@stapp01 ~$
```
successfully logged in to system with user tony.

