Title: OpenSSH Installation & Securing on CentOS 7

Date: 2016-05-13 13:26:17

---

#TL;DR
You may question why do I write a topic that already has so many articles on it. Yes, I'v read a lot guides teaching you on how to install and configure OpenSSH on *nix platforms. But some of them are outdated that don't meet the needs now ('16 Q2). Futher more, most of them are talking about iptables, but not FirewallD and SELinux which are installed and enabled by default on CentOS 7 and RHEL 7 now. So what I'm going to talk about in this guide is how to configure OpenSSH with FirewallD and SELinux. You can jump to section [] if you already familiar with the installation part.

#Installation

Install OpenSSH server:

```
# yum update
# yum install openssh-server
```

Start the service:

```
# systemd start sshd
```

Check if it runs correctly:

```
# ps aux | grep sshd
# netstat -tulpn | grep 22
```

#Securing

Edit OpenSSH configuration file:

```
# vi /etc/ssh/sshd_config
```
Press `i` to start edit.

To disable root logins, edit or add as follows:

```
PermitRootLogin no
```

Change default port (i.e. run it on a non-standard port like 12450)
```
Port 12450
```

Press `ZZ` to save and exit.

Add new port to SELinux

```
# semanage port -a -t ssh_port_t -p tcp 12450
# semanage port -l | grep ssh
    ssh_port_t          tcp      12450,22
```
Add new port to FirewallD

```
# firewall-cmd --zone= --permanent --add-port=12450/tcp
# firewalld-cmd --reload
```
Start OpenSSH service

```
# systemd restart sshd
```

Automatic load on boot

```
# systemd enable sshd
```
