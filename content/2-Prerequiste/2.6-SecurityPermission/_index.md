---
title : "Security and File Permissions"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 2.6 </b> "
---

![Createacloud](/images/2-Prerequiste/6/1.png)

### Linux Account 
![Createacloud](/images/2-Prerequiste/6/3.png)

1. User's informations are stored under /etc/passwd file.

```
$ cat /etc/passwd
```

2. Information about groups is stored into /etc/group file.

```
$ cat /etc/group
```

![Createacloud](/images/2-Prerequiste/6/4.png)

3. The user also has a GID, the group id they are part of, id command can be use to check these details. for eg:

```
$ id ec2-user
uid=1001(ec2-user) gid=1001(ec2-user)groups=1001(ec2-user),1003(developers)
```

4. More details about the user account can be found eg. default shell, home directory using.

```
$ grep -i ec2-user /etc/passwd
ec2-user:x:1001:1001::/home/ec2-user:/bin/sh
```

![Createacloud](/images/2-Prerequiste/6/5.png)

5. To see the list of users currently logged use who command.

```
$ who
bob pts/2 Apr 28 06:48 (172.16.238.187)
```

6. The last command displays the record of all logged-in users along with the date and time when the system was rebooted.

```
$ last
ec2-user :1 :1 Tue May 12 20:00 still logged in
sarah :1 :1 Tue May 12 12:00 still running
reboot system boot 5.3.0-758-gen Mon May 11 13:00 - 19:00 (06:00)
```

### Switching users
![Createacloud](/images/2-Prerequiste/6/6.png)

7. To switch to any user use su command.

```
$ su –
Password:

root ~#
```

8. To run a specific command you can use su -c "whoami" (This is not recommended way)

```
[ec2-user@ubuntu-server ~]$ su -c "whoami"
Password:
root
```

9. To run a command as a root user sudo command is recommended.

```
[ec2-user@ubuntu-server ~]$ sudo apt-get install nginx
[sudo] password for ec2-user:
```
![Createacloud](/images/2-Prerequiste/6/7.png)

10. Users listed in /etc/sudoers file can make use of sudo command for privledge escalation.

```
$ cat /etc/sudoers
```

11. To restrict anyone from directly login as root login, this can be done by setting nologin shell.

```
$ grep -i ^root /etc/passwd
/root:x:0:0:root:/root:/usr/sbin/nologin
```

### User Add
![Createacloud](/images/2-Prerequiste/6/8.png)

12. To create a new local user bob in the system use useradd command.

```
$ useradd bob
```

13. To get more details about bob account like, home director, uid, and shell use /etc/passwd

{{%notice tip%}}
   
Amazon Linux, including Amazon Linux 2 and Amazon Linux AMI, does not support the apt-get package manager as it is based on RPM (Red Hat Package Manager) systems rather than Debian systems which use `apt-get`. Instead, Amazon Linux uses `yum` or `dnf` for package management.
   
{{%/notice%}}

```
$ grep -i bob /etc/passwd
bob:x:1002:1002::/home/bob:/bin/sh
```

14. To check the uid or username of the user logged in user whoami command.

```
$ whoami
bob
```

15. All user's password are store under /etc/shadow

```
$ grep -i bob /etc/shadow
bob:!:18341:0:99999:7:::
```

16. To change the password of current user use passwd or for any specific user use passwd <username>

```
$ passwd bob
Changing password for user bob.
New UNIX password:
Retype new UNIX password:
passwd: all authentication tokens updated
successfully.
```

### Managing Users
![Createacloud](/images/2-Prerequiste/6/9.png)

17. useradd command be used along with many attributes as show below.

```
$ useradd -u 1009 -g 1009 -d /home/robert -s /bin/bash -c ”Mercury Project member" bob
$ id bob
$ grep -i bob /etc/passwd
```

### ACCESS CONTROL FILES
![Createacloud](/images/2-Prerequiste/6/10.png)

18. To get more details about one's account for example bob account, home director, uid, and shell check /etc/passwd

```
$ grep -i ^bob /etc/passwd
bob:x:1002:1002::/home/bob:/bin/sh

USERNAME:PASSWORD:UID:GID:GECOS:HOMEDIR:SHELL
```

19. Password are stored under /etc/shadow

```
$ grep -i ^bob /etc/shadow
bob:$6$0h0utOtO$5JcuRxR7y72LLQk4Kdog7u09LsNFS0yZPkIC8pV9tgD0wXCHutY
cWF/7.eJ3TfGfG0lj4JF63PyuPwKC18tJS.:18188:0:99999:7:::

USERNAME:PASSWORD:LASTCHANGE:MINAGE:MAXAGE:WARN:INACTIVE:EXPDATE
```

20. Check the groups bob belongs too

```
$ grep -i ^bob /etc/group
developer:x:1001:bob,ec2-user

NAME:PASSWORD:GID:MEMBERS
```

### LINUX FILE PERMISSIONS
![Createacloud](/images/2-Prerequiste/6/11.png)

![Createacloud](/images/2-Prerequiste/6/12.png)

### Directory Permission
![Createacloud](/images/2-Prerequiste/6/13.png)

21. To list the directory permission use

```
$ ls -ld /home/bob/random_dir
```

22. To know the current user

```
$ whoami
```

23. To change the change the directory

```
$ cd /home/bob/random_dir
```

### Modifying file permissions
![Createacloud](/images/2-Prerequiste/6/14.png)

**Use `chmod` command to modify the file permissions.**

24. Provide full access to owners

```
$ chmod u+rwx test-file
```

25. Provide Read access to Owners, groups and others, Remove execute access

```
$ chmod ugo+r-x test-file
```

26. Remove all access for others

```
$ chmod o-rwx test-file
```

27. Full access for Owner, add read , remove execute for group and no access for others

```
$ chmod u+rwx,g+r-x,o-rwx test-file
```

### Chomd Permission File
![Createacloud](/images/2-Prerequiste/6/15.png)

28. Provide full access to Owners, group and others

```
$ chmod 777 test-file
```

29. Provide Read and execute access to Owners,groups and others

```
$ chmod 777 test-file
```

30. Read and Write access for Owner and Group, No access for others.

```
$ chmod 660 test-file
```

31. Full access for Owner, read and execute for group and no access for others.

```
$ chmod 750 test-file
```

### Change Ownership
![Createacloud](/images/2-Prerequiste/6/16.png)

32. Changes owner to bob and group to developer

```
$ chown bob:developer test-file
```

33. Changes just the owner of the file to bob. Group unchanged.

```
$ chown bob andoid.apk
```

34. Change the group for the test-file to the group called android.

```
$ chgrp android test-file
```

### SSH
![Createacloud](/images/2-Prerequiste/6/17.png)

35. To login to the remote server use ssh command with hostname or IP address.

```
ssh <hostname OR IP Address>
```

36. To login to the remote server with specific username and password.

```
ssh <user>@<hostname OR IP Address>
```

37. `-l` attribute can also be used as

```
ssh –l <user> <hostname OR IP Address>
```

### Password-Less Authentication
![Createacloud](/images/2-Prerequiste/6/18.png)

38. To generate a keypair on the Client run this command

```
$ ssh-keygen –t rsa
```

39. Public and Private key are stored at below location.

```
Public Key: /home/bob/.ssh/id_rsa.pub

Private Key: /home/bob/.ssh/id_rsa
```

### SCP
![Createacloud](/images/2-Prerequiste/6/19.png)

40. To copy a compresses file to a remote server

```
$ scp /home/bob/caleston-code.tar.gz devapp01:/home/bob
```

41. To copy a directory to a remote server

```
$ scp –pr /home/bob/media/ devapp01:/home/bob
```
