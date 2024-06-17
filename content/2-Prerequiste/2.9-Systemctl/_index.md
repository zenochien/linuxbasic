---
title : "Service Management with SYSTEMD"
date : "`r Sys.Date()`"
weight : 9
chapter : false
pre : " <b> 2.9 </b> "
---

### Systemctl Commands
![Createacloud](/images/2-Prerequiste/9/1.png)

1. To start a service use the start command, for example to start a docker service use systemctl start docker

```
$ systemctl start docker
```

2. To stop a service use the stop command, for example to stop a docker service use systemctl stop docker

```
$ systemctl stop docker
```

3. To restart a service use the restart command, for example to restart a docker service use systemctl restart  docker this will stop and start again.

```
$ systemctl restart docker
```

4. To reload a service use the reload command, for example to reload a docker service use systemctl reload docker, this will reload all the configuration without interrupting the normal functionaltiy of the service

```
$ systemctl reload docker
```

5. To enable a service and make it persistent accross reboots use the enable command, for example to enable a docker service use systemctl enable docker

```
$ systemctl enable docker
```

6. To disable a service at boot use the disable command, for example to disable a docker service use systemctl disable docker command.

```
$ systemctl disable docker
```

7. To know the status of the service use systemctl status docker command. This command provided the state of the service. If running properly is should show active (running) state as shown in screenshot below.

```
$ systemctl status docker
```

![Createacloud](/images/2-Prerequiste/9/2.png)

8. To see the current runlevel use systemctl get-default

```
$ systemctl get default
```

9. To change the runleve to a different target use systemctl set-default multi-user.target

```
$ systemctl set-default multi-user.target
```

10. To list all the units that systemd has loaded use systemctl list-units --all, this lists all the unit which are active, inactive or anyother state.

```
$ systemctl list-units --all
```

11. To list only active units use systemctl list-units command

```
$ systemctl list-units
```

### JOURNALCTL
![Createacloud](/images/2-Prerequiste/9/3.png)

13. Using journalctl commands print all the log entries from oldest to the newest.

```
$ journalctl
```

14. Using journalctl -b command print all the logs from the current boot.

```
$ journalctl -b
```

15. Using journalctl -u docker.service command print all the logs specific to the unit specified, for example docker in this case.

```
$ journalctl -u docker.service
```

16. Using journalctl -u docker.service --since command print all the logs specific to the unit specified since the given time, for example docker in this case.

```
$ journalctl -u docker.service --since "2022-01-01 13:45:00"
```