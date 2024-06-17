---
title : "Working with Shell Basic"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

#### **Working with Shell Basic**

1. Our goal is to create a directory structure, the top most directory which is ``/home/ec2-user/environment`` which is already created as it as a home directory but everything else underneath has to be created.

![Createacloud](/images/2-Prerequiste/2/2.png)

1. To print the present working directory. Run pwd command

```
$ pwd
```

2. To see the contents of the directory. Run ls command

```
$ ls
```

3. To make (or) create a directory. Run mkdir command

```
$ mkdir Asia
```

4. To make (or) create multiple directories. Run mkdir command followed by <directory_name1> <directory_name2> .. <directory_nameN>

```
$ mkdir Europe Africa America
```

5. To change a directory from the current directory. Run cd <directory_name>

```
$ cd Asia
```

6. To recursively created directories. Run mkdir -p <directory_name1>/<sub_directory_of_name1>

```
$ mkdir -p India/Mumbai
```

7. To go back to one directory up. Run cd ..

```
$ cd ..
```

8. To go back directly to a home directory of the current user from any location in the system. Run cd

```
$ cd
```

![Createacloud](/images/2-Prerequiste/2/3.png)
9. To change to a directory with absolute path. Run cd <directory_path>

```
$ cd /home/michael
```

10. To Change to a directory with relative path. Run cd <directoryName>

```
$ cd Asia
```
![Createacloud](/images/2-Prerequiste/2/4.png)

11. To move file or directory. Run mv <source> <destination> command

```
$ mv /home/ec2-user/environment/michael/Europe/Morocco /home/michael/Africa/
**or**
$ mv Europe/Morocco Africa/
```

12. To rename a directory. Run mv <oldname> <newname> command

```
$ mv Asia/India/Munbai Asia/India/Mumbai
```

13. To copy a file to a directory. Run cp <filename> <destination_directorypath> command

```
$ cp Asia/India/Mumbai/City.txt Africa/Egypt/Cairo
```

14. To delete a file from a directory. Run rm /path/<filename> command

```
$ rm Europe/UK/London/Tottenham.txt
```

15. To copy a directory recursively. Run cp -r <sourcepath> <destinationPath> command

```
$ cp -r Europe/UK Europe/UnitedKingdom
```

16. To print the content of a file. Run cat /path/to/<filename> command

```
$ cat Asia/India/Mumbai/City.txt
```

17. To add a content to a file with cat(redirect) . Run cat > /path/to/<filename> command

```
$ cat > Africa/Egypt/Cairo/City.txt
  Cairo
  `Type Ctrl + d from keyboard`
```
18. To create an empty file. Run touch /path/to/filename command

```
$ touch /Asia/China/Country.txt
```

19. To get the long list of files and directories. Run ls -l command

```
$ ls -l
```

20. To list all files including the hidden. Run ls -la command

```
$ ls -a
```

21. To list all the files in the order they were modified. Run ls -lt command

```
$ ls -lt
```

22. To list all the files form oldest to newest. Run ls -ltr command

```
$ ls -ltr
```

23. To check the home directory for a particular user say bob

```
$ grep bob /etc/passwd | cut -d ":" -f6
```

24. To check the home directory for a particular user using built in shell variables

```
$ echo $HOME
```

25. In the command echo Welcome, what does the word Welcome represent with respect to the command?

```
$ echo Welcome 
  - Where Welcome is an argument
```

26. To check git command type

```
$ type git
```

27. To create a directory

```
$ mkdir /home/ec2-user/environment/birds
```

28. To create directories recursively

```
$  mkdir -p /home/ec2-user/environment/fish/salmon
```

29. Create few more directories

```
$ mkdir -p /home/ec2-user/environment/mammals/elephant
$ mkdir -p /home/ec2-user/environment/mammals/monkey
$ mkdir /home/ec2-user/environment/birds/eagle
$ mkdir -p /home/ec2-user/environment/reptile/snake
$ mkdir -p /home/ec2-user/environment/reptile/frog
$ mkdir -p /home/ec2-user/environment/amphibian/salamander
```

30. To move a directory

```
$ mv /home/ec2-user/environment/reptile/frog /home/ec2-user/environment/amphibian
```

31. To rename a directory

```
$ mv /home/ec2-user/environment/reptile/snake /home/ec2-user/environment/reptile/crocodile
```

32. To delete a directory

```
$ rm -r /home/ec2-user/environment/reptile
```

### Bash environment variables
![Createacloud](/images/2-Prerequiste/2/6.png)

33. To print SHELL environment variable

```
$ echo $SHELL
```

34. To see a list of all environment variables. Run env from the terminal

```
$ env
```

35. To set an environment variable with in the shell. The value is not carry forward to any other process.

```
$ OFFICE=caleston
```

36. To set an environment variable we can use the export command. To make the value carry forward to any other process.

```
$ export OFFICE=caleston
```

37. To persistently set an environment variable over subsequent login or a reboot add them to the ~/.profile or ~/.pam_environment in the users home directory.

```
$ echo "export OFFICE=caleston" >> ~/.profile 
**or**
$ echo "export OFFICE=caleston" >> ~/.pam_environment
```

38. To check the value of a environment variable called LOGNAME

```
$ echo $LOGNAME
```

### Path Variable
![Createacloud](/images/2-Prerequiste/2/7.png)

39. To see the directories defined in path variable. Use the command echo $PATH.

```
$ echo $PATH
```

40. To check if the location of the command can be identified. Use the which command ``Syntax: which <command>``

```
$ which obs-studio
```

41. To define a command in the PATH variable. To add we can use the export command.

```
$ export PATH=$PATH:/opt/obs/bin
$ which obs-studio
```

### Customize Bash Prompt
![Createacloud](/images/2-Prerequiste/2/8.png)

42. To see the value assign to PS1, type echo $PS1

```
$ echo $PS1
```

43. To change the PS1 to only display the word ubuntu-server.

```
$ PS1="ubuntu-server"
$ echo $PS1
```

### To customize further, have a look at the below special character.
![Createacloud](/images/2-Prerequiste/2/9.png)

44. To change the bash prompt to display **date**, **time**, **username of the current user**, the **hostname** and **the current working directory**

```
$ PS1="[\d \t \u@\h:\w ] $ "
```

