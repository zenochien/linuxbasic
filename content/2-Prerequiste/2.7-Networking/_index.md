---
title : "Netwoking"
date : "`r Sys.Date()`"
weight : 7
chapter : false
pre : " <b> 2.7 </b> "
---

### Ping
![Createacloud](/images/2-Prerequiste/7/1.png)

1. Ping Command is use to check the remote machine is reachable or not.

```
$ ping 192.168.1.11
Reply from 192.168.1.11: bytes=32 time=4ms TTL=117
Reply from 192.168.1.11: bytes=32 time=4ms TTL=117
```

2. To Ping the remote host with a name instead of IP Address make an entry in /etc/hosts file

```
$ ping db
ping: unknow host db
```

3. To Ping the remote host with a name instead of IP Address make an entry in /etc/hosts file
![Createacloud](/images/2-Prerequiste/7/2.png)

```
$ cat >> /etc/hosts
192.168.1.11 db
```
```
$ ping db
PING db (192.168.1.11) 56(84) bytes of data.
64 bytes from db (192.168.1.11): icmp_seq=1 ttl=64 time=0.052 ms
64 bytes from db (192.168.1.11): icmp_seq=2 ttl=64 time=0.079 ms
```

### Name Resolution
![Createacloud](/images/2-Prerequiste/7/3.png)

![Createacloud](/images/2-Prerequiste/7/4.png)

### DNS

The domain name system is a distributed way to share these name-to-IP associations instead of requiring each computer to synchronize a hosts file. A name server publishes the IP address for a domain and provides a single location to update when an IP changes.

![Createacloud](/images/2-Prerequiste/7/5.png)

![Createacloud](/images/2-Prerequiste/7/6.png)

### DOMAIN NAMES
![Createacloud](/images/2-Prerequiste/7/7.png)

![Createacloud](/images/2-Prerequiste/7/8.png)

- .com - Commerical or General Purpose.
- .net - Network or General Purpose.
- .edu - Education Purpose
- .org - Organizations for non profit organizations etc.

### Record Types
![Createacloud](/images/2-Prerequiste/7/9.png)

- A - IP to host names.
- AAAA - Storing ipv6 to hostnames.
- CNAME - Mapping one name to another.

4. To test the DNS resolution you can use nslookup command, this will query a hostname from a DNS Server.
![Createacloud](/images/2-Prerequiste/7/10.png)

```
$ nslookup www.google.com
Server: 8.8.8.8
Address: 8.8.8.8#53
Non-authoritative answer:
Name: www.google.com
Address: 172.217.0.132
```

5. Another useful tool to query a hostname from a DNS server is dig which return more detailed information as shown.
![Createacloud](/images/2-Prerequiste/7/11.png)

```
$ dig www.google.com
; <<>> DiG 9.10.3-P4-Ubuntu <<>> www.google.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 28065
;; flags: qr rd ra; QUERY: 1, ANSWER: 6, AUTHORITY: 0, ADDITIONAL: 1
;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;www.google.com. IN A
;; ANSWER SECTION:
www.google.com. 245 IN A 64.233.177.103
www.google.com. 245 IN A 64.233.177.105
www.google.com. 245 IN A 64.233.177.147
www.google.com. 245 IN A 64.233.177.106
www.google.com. 245 IN A 64.233.177.104
www.google.com. 245 IN A 64.233.177.99
;; Query time: 5 msec
;; SERVER: 8.8.8.8#53(8.8.8.8)
;; WHEN: Sun Mar 24 04:34:33 UTC 2019
;; MSG SIZE rcvd: 139
```

### Switching
![Createacloud](/images/2-Prerequiste/7/12.png)

6. To see the interfaces on the hosts use ip link command

```
$ ip link
eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode
DEFAULT group default qlen 1000
```

7. To connect to the switch we use ip addr add command

```
$ ip addr add 192.168.1.10/24 dev eth0
```

### Default Gateway
![Createacloud](/images/2-Prerequiste/7/13.png)
![Createacloud](/images/2-Prerequiste/7/14.png)
![Createacloud](/images/2-Prerequiste/7/15.png)


8. To configure a gateway on system B to reach the system on other network run

```
$ ip route add 192.168.1.0/24 via 192.168.2.1
```

9. To see the existing routing table configuration run the route command.

```
$ route
```

### Check Interfaces
![Createacloud](/images/2-Prerequiste/7/16.png)

10. Use the ip link to ensure the primary interface is up.

```
$ ip link
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc
    noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp1s0f1: <BROADCAST,BROADCAST,MULTICAST,UP> mtu 1500 qdisc
    fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 08:97:98:6e:55:4d brd ff:ff:ff:ff:ff:ff
```

11. Check if we can resolve the hostname to IP address via nslookup
![Createacloud](/images/2-Prerequiste/7/17.png)

```
$ nslookup caleston-repo-01
Server:      192.168.1.100
Address:     192.168.1.100 #53

Non-authoritative answer:
Name: caleston-repo-01
Address: 192.168.2.5
```

12. `ping` to check the connectivity.
![Createacloud](/images/2-Prerequiste/7/18.png)

```
$ ping caleston-repo-01
PING caleston-repo-01 (192.168.2.5) 56(84) bytes of data.

--- localhost ping statistics ---
3 packets transmitted, 0 received, 100% packet loss, time 2034ms
```

13. `traceroute` to check the number of hops between the source.
![Createacloud](/images/2-Prerequiste/7/19.png)

```
$ traceroute 192.168.2.5

Tracing route to example.com [192.168.2.5]
over a maximum of 30 hops:
1 <1 ms <1 ms <1 ms 192.168.1.1
2 <2 ms <1 ms <1 ms 192.168.2.1
3 * * * Request timed out.
```

14. To check the port status use `netstat` command and to use it along with port number use below command.
![Createacloud](/images/2-Prerequiste/7/20.png)

```
$ netstat -an | grep 80 | grep -i LISTEN
```