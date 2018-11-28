# Tunning OS
Tuning of the Linux operating system has been done "out of the box" by enterprise-optimized distributions, but there are still many opportunities for a system administrator to improve the performance of his or her workload on a Linux system.
A number of kernel tuning suggestions, mainly in terms of ports and socket descriptors.
Some concepts about tunning as following:
+ File Handle Limits
+ Socket Tuning
+ Process Scheduler
+ Filesystem Tuning

This lab, assumption using OS as centos 7 as following.

## Edit /etc/security/limits.conf
```
*               soft    nofile          20000000
*               hard    nofile          20000000
root            soft    nofile          20000000
root            hard    nofile          20000000
```
You should reboot your os
-> after reboot, you can login and check by command:
```
[root@ ~]# ulimit -n
20000000
```
## You should edit file handle limit, socket tunning as this file /etc/sysctl.conf
```
fs.file-max = 20000000
fs.nr_open = 20000000
net.ipv4.ip_local_port_range = 1024 65535
net.ipv4.tcp_tw_recycle = 1
net.ipv4.tcp_tw_reuse = 1
net.ipv4.tcp_max_syn_backlog = 32400000
net.ipv4.tcp_max_tw_buckets = 20000000
net.ipv4.tcp_fin_timeout = 15
net.ipv4.tcp_keepalive_intvl = 30
net.ipv4.tcp_keepalive_probes = 5
net.ipv4.tcp_mem = 383865 511820 2303190

net.core.rmem_max = 16777216
net.core.wmem_max = 16777216
```

Run below command for modifying kernel parameters.
```
sysctl -p 
```

# Reference
```
[1]. http://www.tweaked.io/guide/kernel/
[2]. https://mrotaru.wordpress.com/2013/10/10/scaling-to-12-million-concurrent-connections-how-migratorydata-did-it/
[3]. https://gist.github.com/sokratisg/98d03e20fca76d4b699f
[4]. https://www.cyberciti.biz/faq/linux-increase-the-maximum-number-of-open-files/
[5]. https://easyengine.io/tutorials/linux/sysctl-conf/
```

