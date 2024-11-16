title: Fix Bad Ownership or Modes for SSH Public-keys

date: 2016-02-21 20:01:44
---
Check secure log:

    $tail -f /var/log/secure

    Dec 13 09:38:52 Inazuma-KaiNi sshd[1857]: Authentication refused: bad ownership or modes for directory /home/Explorare/.ssh

Check the ownership and modes to `/.ssh`

    $ls -la $HOME/.ssh

    total 10
    rwxrwx---+ 1 Explorare Explorare    0 Dec 13 21:44 .
    rwxrwxr-x+ 1 Explorare Explorare    0 Dec 13 22:46 ..
    rw-rwxr--+ 1 Explorare Explorare  406 Dec 13 17:36 authorized_keys

**The permissions to the `authorized_keys` is being more permissive than sshd allows by defalut.** [\[1\]](#R1)

In this case, it can be solved by executing the following on the server.

    #chmod 700 ~/.ssh
    #chmod 600 ~/.ssh/authorized_keys

Check again.

    rwx------+ 1 Explorare Explorare    0 Dec 13 21:44 .
    rwx------+ 1 Explorare Explorare    0 Dec 13 22:46 ..
    rw-------+ 1 Explorare Explorare  406 Dec 13 17:36 authorized_keys

<!--more-->

There is also another situation:

    rwx------+ 1 root      root    0 Dec 13 21:44 .
    rwx------+ 1 Explorare Explorare    0 Dec 13 22:46 ..
    rw-------+ 1 root      root  406 Dec 13 17:36 authorized_keys

This usually happened when using root account to setup public-key authentication for other users. So the ownership to `./ssh` is `root` which cause permission denied.

In this case, it can be solved by excuting the flowwing on the server.

    chown `whoami` ~/.ssh
    chown `whoami` ~/.ssh/authorized_keys

Check again.

    rwx------+ 1 Explorare root    0 Dec 13 21:44 .
    rwx------+ 1 Explorare Explorare    0 Dec 13 22:46 ..
    rw-------+ 1 Explorare root  406 Dec 13 17:36 authorized_keys

Now the problem should be fixed.

**Ohter useful commands:**

Check SSH client output:

    ssh -i myPublicKey <whoami>@**.**.**.** -p <port>-vvvv

Check SSH server output:

    cat -n /var/log/audit/audit.log

Check SELinux Configuration

`sestatus`：Check current SELinux status

`echo 0 > /selinux/enforce`: Temporarily disable selinux enforcement

Close SELinux (**Not Recommended**): Edit `/etc/sysconfig/selinux`

    SELINUX=permissive --> SELINUX=disabled

Check SSH server configuration

    cat -n /etc/ssh/sshd_config

-------------------------

**References:**

<a id="R1">[1]</a> [OpenSSH FAQ](http://www.openssh.com/faq.html#3.14)

\[2] [HowTos/Network/SecuringSSH - CentOS Wiki](https://wiki.centos.org/HowTos/Network/SecuringSSH#head-9c5717fe7f9bb26332c9d67571200f8c1e4324bc)

\[3] [chmod Man Page | Bash | SS64.com](http://ss64.com/bash/chmod.html)