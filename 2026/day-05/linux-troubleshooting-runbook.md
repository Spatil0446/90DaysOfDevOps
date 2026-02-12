# Day 05 – Linux Troubleshooting Runbook

## Target Service / Process
Service Selected: ssh (OpenSSH Server)
Process Checked: sshd

Reason: SSH is a critical access service. If it fails, remote access is lost.

---

# 1️⃣ Environment Basics

## 1. uname -a

$ uname -a
root@vagrant:/home/vagrant# uname -a
Linux vagrant 4.15.0-58-generic #64-Ubuntu SMP Tue Aug 6 11:12:41 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux

Observation:
System is running Ubuntu with 5.15 kernel. Architecture is x86_64.

---

## 2. lsb_release -a

$ lsb_release -a
root@vagrant:/home/vagrant# lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 18.04.3 LTS
Release:        18.04
Codename:       bionic

Observation:
LTS version – stable production-friendly OS.

---

# 2️⃣ Filesystem Sanity Check

## 3. Create test directory & copy file

root@vagrant:/home/vagrant# mkdir /tmp/runbook-demo
root@vagrant:/home/vagrant# cp /etc/hosts /tmp/runbook-demo/hosts-cop
root@vagrant:/home/vagrant# ls -l /tmp/runbook-demo
total 4
-rw-r--r-- 1 root root 198 Feb 12 04:26 hosts-cop

Observation:
Filesystem writable. No permission or disk errors.

---

## 4. df -h

root@vagrant:/home/vagrant# df -h
Filesystem                    Size  Used Avail Use% Mounted on
udev                          463M     0  463M   0% /dev
tmpfs                          99M  5.1M   94M   6% /run
/dev/mapper/vagrant--vg-root   62G  1.6G   58G   3% /
tmpfs                         493M     0  493M   0% /dev/shm
tmpfs                         5.0M     0  5.0M   0% /run/lock
tmpfs                         493M     0  493M   0% /sys/fs/cgroup
vagrant                       475G  109G  367G  23% /vagrant
tmpfs                          99M     0   99M   0% /run/user/1000
Observation:
Root filesystem 3% used – healthy, no disk pressure.

---

# 3️⃣ CPU & Memory Snapshot

## 5. ps -o pid,pcpu,pmem,comm -p $(pgrep sshd)

root@vagrant:/home/vagrant# ps -o pid,pcpu,pmem,comm -p 13336
  PID %CPU %MEM COMMAND
13336  0.0  0.0 pager

Observation:
pager using negligible CPU and low memory.

---

## 6. free -h

root@vagrant:/home/vagrant# free -h
              total        used        free      shared  buff/cache   available
Mem:           985M         75M        375M        5.0M        535M        759M
Swap:          979M          0B        979M

Observation:
Plenty of free memory. No swap usage. System not memory stressed.

---

# 4️⃣ Disk & IO

## 7. du -sh /var/log

root@vagrant:/home/vagrant# du -sh /var/log
33M     /var/log

Observation:
Log directory size normal. No abnormal growth.

---

## 8. vmstat 1 3

root@vagrant:/home/vagrant# vmstat 1 3
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 1  0      0 384064  32116 515956    0    0     9     3   12   32  0  0 100  0  0
 0  0      0 384064  32116 515940    0    0     0     0   21   42  0  0 100  0  0
 0  0      0 384064  32116 515940    0    0     0     0   19   32  0  0 100  0  0

Observation:
CPU idle ~100%. No IO wait. System healthy.

---

# 5️⃣ Network Snapshot

## 9. ss -tulpn | grep ssh

root@vagrant:/home/vagrant# ss -tulpn | grep ssh
tcp    LISTEN   0        128                0.0.0.0:22            0.0.0.0:*      users:(("sshd",pid=960,fd=3))          
tcp    LISTEN   0        128                   [::]:22               [::]:*      users:(("sshd",pid=960,fd=4)) 

Observation:
SSH listening on port 22 on all interfaces.


---

# 6️⃣ Logs Reviewed

## 11. journalctl -u ssh -n 50

root@vagrant:/home/vagrant# journalctl -u ssh -n 50
-- Logs begin at Wed 2026-02-04 15:38:57 UTC, end at Thu 2026-02-12 04:17:01 UTC. --
Feb 04 15:39:04 vagrant systemd[1]: Starting OpenBSD Secure Shell server...
Feb 04 15:39:04 vagrant sshd[960]: Server listening on 0.0.0.0 port 22.
Feb 04 15:39:04 vagrant sshd[960]: Server listening on :: port 22.
Feb 04 15:39:04 vagrant systemd[1]: Started OpenBSD Secure Shell server.
Feb 04 15:39:05 vagrant sshd[983]: Accepted publickey for vagrant from 10.0.2.2 port 51144 ssh2: RSA SHA256:1M4RzhMyWuFS
Feb 04 15:39:05 vagrant sshd[983]: pam_unix(sshd:session): session opened for user vagrant by (uid=0)
Feb 04 15:39:13 vagrant sshd[1309]: Accepted publickey for vagrant from 10.0.2.2 port 54922 ssh2: ED25519 SHA256:gW6kHTW
Feb 04 15:39:13 vagrant sshd[1309]: pam_unix(sshd:session): session opened for user vagrant by (uid=0)
Feb 04 15:40:05 vagrant sshd[1496]: Accepted publickey for vagrant from 10.0.2.2 port 61508 ssh2: ED25519 SHA256:gW6kHTW
Feb 04 15:40:05 vagrant sshd[1496]: pam_unix(sshd:session): session opened for user vagrant by (uid=0)

Observation:
Recent successful login entries. No authentication errors.






