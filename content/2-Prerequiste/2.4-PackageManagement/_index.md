---
title : "Package Management"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 2.4 </b> "
---
![Createacloud](/images/2-Prerequiste/4/1.png)

### Introduction to Package Managers
![Createacloud](/images/2-Prerequiste/4/2.png)

For **Debain/Ubuntu**, it is **apt/dpkg** and for CentOs/Redhat, it is **RPM**

**Question** : What is the difference between `CentOS`, `RHEL` and `Ubuntu`*?
![Createacloud](/images/2-Prerequiste/4/3.png)

- There are hundreds of Linux distributions in use today

One of the common ways to catagorize linux distribution is by the package manager it uses.

- For example: Distributions such as `RHEL`, `Fedora` and `CentOS`. are based on RPM. Hence they are known as `RPM` based distribution. The Debian family including `Ubuntu`, `Debian` and `Linux Mint` e.t.c. make use of Debian based package managers such as the `DPKG`.

![Createacloud](/images/2-Prerequiste/4/4.PNG)

### What is a package?

- A package in its simplest defination is a compressed archieve that contains all the files that are required by a particular software to run.
- For example: Lets consider an Ubuntu System, we want to install a simple editing system such as gimp which stands for  GNU Image Manipulation System. To do this, we can make use of the **gimp.deb** package which contains all the software binaries and files needed to for the image editor to run along with the metadata which provides the information about the software itself.

![Createacloud](/images/2-Prerequiste/4/5.png)

### Types of Package Managers

![Createacloud](/images/2-Prerequiste/4/6.png)

### RPM (Redhat Package Manager)

![Createacloud](/images/2-Prerequiste/4/7.PNG)

RPM has five basic modes of operations. Each of these modes can be run using rpm command followed by a specific command options. Despite of this, RPM doesn't resolve dependencies on its own. This is why we make use of a higher level of package manager called `YUM`.

- Installing

- Uninstalling

- Upgrade

- Query

- Verfiying

- rpm-modes

### YUM (Yellowdog Updater Modifier)

YUM is a free and opensource package manager.

- Works on RPM based Linux systems

- Works with Software repositories which are essentially a collection of packages and provides package independency management on RPM based distro. The repository information is stored in `/etc/yum.repos.d/` and repository files will have the `.repo` extension.

- Acts as a high level package manager but under the hood it still depeneds on `RPM` to manage packages on the linux systems.

- Unlike RPM, YUM handles package dependencies very well (Automatic Dependency Resolution). It is able to install any dependencies packages to get the base package install on the linux system.

![Createacloud](/images/2-Prerequiste/4/9.PNG)

- Once yum runs `sudo yum install httpd` command is issued YUM first runs transaction check, if the package is not installed in the system yum checks the configured repositories under `/etc/yum.repos.d/` for the availability of the requested package.

- It also checks if there are any dependent packages are already installed in the system or if it needs to be upgrade.

![Createacloud](/images/2-Prerequiste/4/10.PNG)

- After this step, transaction summary is displayed on the screen for the user to review, if we wish to proceed with the install enter the `y` button (this step can be skipped by providing the `-y` flag with the `yum install` command).

- Yum will download and install necessary RPMs to linux system

![Createacloud](/images/2-Prerequiste/4/11.PNG)

- If you want to install or update a single package, use `sudo yum install telnet` and `sudo yum update telnet` command. If the package is already in the latest version in the repository and hence no action will be taken

![Createacloud](/images/2-Prerequiste/4/12.PNG)

### Common Commands

1. To list all the repos added to your system. Run yum repolist

```
$ yum repolist
```

2. To check which package should be installed for specific command to work. Use yum provides command followed by name.

```
$ yum provides scp
```

3. To Install a package

```
$ sudo yum install httpd
```

4. To Install a package to automatically answer **"yes"** to any question prompt during the operation. Use `-y` flag with the yum install command.

```
$ sudo yum install httpd -y
```

5. To remove a package

```
$ sudo yum remove httpd
```

6. To update a package

```
$ sudo yum update telnet
```

7. To update all packages in the system, use the yum update command without any arguments.

```
$ sudo yum update
```

### Lab - RPM and YUM

8. Use an rpm command and find out the exact package name for wget installed in this server

```
$ rpm -qa |grep wget
```

9. To install a package for firefox browser that has been downloaded under /home/bob in the system. Caution: It might fail due to failed dependencies

```
$ sudo rpm -ivh /home/bob/firefox-68.6.0-1.el7.centos.x86_64.rpm
```

10. To install a package for firefox browser along with its dependencies

```
$ sudo yum install firefox -y
```

11. To check how many software repositories are configured for YUM in the system

```
$ sudo yum repolist
```

12. To check which package provides tcpdump command

```
$ sudo yum provides tcpdump
```

### APT and APT-GET 
{{%notice tip%}}
   
Amazon Linux, including **Amazon Linux 2** and Amazon Linux AMI, does not support the apt-get package manager as it is based on **RPM (Red Hat Package Manager)** systems rather than Debian systems which use `apt-get`. Instead, Amazon Linux uses `yum` or `dnf` for package management.
   
{{%/notice%}}

13. To refresh a repository. Run apt update command.
![Createacloud](/images/2-Prerequiste/4/13.png)

```
$ sudo apt update
```

14. To install available upgrades of all packages currently installed on the system from the sources configured.

```
$ sudo apt upgrade
```

15. Another way to update the repository is to use apt edit-sources command. This opens up the /etc/apt/sources.list file in the text editor of your choice.

```
$ sudo apt edit-sources
```

![Createacloud](/images/2-Prerequiste/4/14.png)

16. To install the package

```
$ sudo apt install telnet
```

17. To remove the package

```
$ sudo apt remove telnet
```

18. To search or look for a package in the repository.

```
$ sudo apt search telnet 
```

19. To list all the available packages

```
$ sudo apt list |grep telnet
```

**Difference between APT vs APT-GET**
- APT is a more user friendly tool when compared to APT-GET
- In all the latest debian based distros APT is already installed by default.

**Lets try to install firefox package using both APT and APT-GET**
- You will notice APT does easy on the eyes, you get just enough information and also a nice little progress bar
- APT-GET is just effective and doesn't provide the output in user-friendly format.

![Createacloud](/images/2-Prerequiste/4/15.PNG)

**Another comparision by search a telent package.**
- You will notice with apt, all its options are located in one place. You can search with apt search telnet command.
- On the other hand, you cannot use search command with apt-get command. Instead, you have to use another tool called apt-cache search telnet.
- If you compare the results of the two commands, you will also see the apt-cache throws in a lot of extra information in the search result, which may not be really useful for the end user.
![Createacloud](/images/2-Prerequiste/4/16.PNG)

### Lab - DPKG and APT

20. To install a package for firefox browser which has been downloaded at /root/firefox.deb. The dependencies might fail.

```
$ sudo dpkg -i /root/firefox.deb
```

21. To install a package using APT

```
$ sudo apt install firefox
```

22. The package to install Chromium browser in the system. Use apt search functionality to locate the correct package name. The browser has the description of: Chromium web browser, open-source version of Chrome

```
$ sudo apt search chromium-browser
```

23. To install the chromium-browser

```
sudo apt install -y chromium-browser
```

24. To remove the firefox browser from the system.

```
$ sudo apt remove firefox
```
