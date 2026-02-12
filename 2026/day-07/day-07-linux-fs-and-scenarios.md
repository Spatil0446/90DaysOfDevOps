# Day 07 – Linux File System Hierarchy & Scenario Practice

---

#  Part 1 – Linux File System Hierarchy

## 1️⃣ / (Root)

Description:
The top-level directory. Everything in Linux starts from `/`.

Command:
root@vagrant:/home/vagrant# ls -l /
total 96
drwxr-xr-x   2 root    root     4096 Aug 15  2019 bin
drwxr-xr-x   3 root    root     4096 Aug 15  2019 boot
drwxr-xr-x  18 root    root     3800 Feb  4 15:38 dev
drwxr-xr-x  95 root    root     4096 Feb  8 03:46 etc
drwxr-xr-x   3 root    root     4096 Feb  8 03:53 home
lrwxrwxrwx   1 root    root       33 Aug 15  2019 initrd.img -> boot/initrd.img-4.15.0-58-generic
lrwxrwxrwx   1 root    root       33 Aug 15  2019 initrd.img.old -> boot/initrd.img-4.15.0-58-generic
drwxr-xr-x  21 root    root     4096 Aug 15  2019 lib
drwxr-xr-x   2 root    root     4096 Aug 15  2019 lib64
drwx------   2 root    root    16384 Aug 15  2019 lost+found
drwxr-xr-x   3 root    root     4096 Aug 15  2019 media
drwxr-xr-x   2 root    root     4096 Aug  5  2019 mnt
drwxr-xr-x   3 root    root     4096 Aug 15  2019 opt
dr-xr-xr-x 108 root    root        0 Feb  4 15:39 proc
drwx------   2 root    root     4096 Feb  8 03:53 root
drwxr-xr-x  27 root    root      980 Feb  7 06:25 run
drwxr-xr-x   2 root    root    12288 Feb  4 15:39 sbin
drwxr-xr-x   2 root    root     4096 Aug 15  2019 snap
drwxr-xr-x   2 root    root     4096 Aug  5  2019 srv
dr-xr-xr-x  13 root    root        0 Feb  4 15:38 sys
drwxrwxrwt   9 root    root     4096 Feb 12 04:26 tmp
drwxr-xr-x  10 root    root     4096 Aug 15  2019 usr
drwxrwxrwx   1 vagrant vagrant  8192 Feb  4 15:38 vagrant
drwxr-xr-x  13 root    root     4096 Aug 15  2019 var
lrwxrwxrwx   1 root    root       30 Aug 15  2019 vmlinuz -> boot/vmlinuz-4.15.0-58-generic
lrwxrwxrwx   1 root    root       30 Aug 15  2019 vmlinuz.old -> boot/vmlinuz-4.15.0-58-generic

I would use this when:
Navigating the system structure or checking mounted directories.

---

## 2️⃣ /home

Description:
Contains personal directories for normal users.

Command:
ls -l /home

Observed:
root@vagrant:/home/vagrant# ls -l /home
total 8
-rwxr-xr-x 1 root    root      73 Feb  8 03:53 test.sh
drwxr-xr-x 6 vagrant vagrant 4096 Feb 12 04:35 vagrant

I would use this when:
Checking user files, scripts, or troubleshooting permission issues.

---

## 3️⃣ /root

Description:
Home directory of the root (superuser).

Command:
ls -l /root

Observed:
root@vagrant:/home/vagrant# ls -l /root
total 0

I would use this when:
Performing administrative tasks as root user.

---

## 4️⃣ /etc

Description:
Stores system-wide configuration files.

Command:
ls -l /etc | head

Observed:
root@vagrant:/home/vagrant# ls -l /etc | head
total 812
drwxr-xr-x 3 root root       4096 Aug 15  2019 acpi
-rw-r--r-- 1 root root       3028 Aug  5  2019 adduser.conf
drwxr-xr-x 2 root root       4096 Aug 15  2019 alternatives
drwxr-xr-x 3 root root       4096 Aug 15  2019 apm
drwxr-xr-x 3 root root       4096 Aug 15  2019 apparmor
drwxr-xr-x 9 root root       4096 Aug 15  2019 apparmor.d
drwxr-xr-x 3 root root       4096 Aug 15  2019 apport
drwxr-xr-x 7 root root       4096 Aug 15  2019 apt
-rw-r----- 1 root daemon      144 Feb 20  2018 at.deny

I would use this when:
Editing service configurations or system settings.

---

## 5️⃣ /var/log

Description:
Contains log files (critical for DevOps troubleshooting).

Command:
ls -l /var/log

Observed:
root@vagrant:/home/vagrant# ls -l /var/log
total 364
drwxr-xr-x  2 root      root              4096 Aug 15  2019 apt
-rw-r-----  1 syslog    adm               7449 Feb 12 04:17 auth.log
-rw-rw----  1 root      utmp                 0 Aug  5  2019 btmp
drwxr-xr-x  2 root      root              4096 Jun 19  2019 dist-upgrade
-rw-r--r--  1 root      root             32064 Feb  8 03:42 faillog
drwxr-sr-x+ 4 root      systemd-journal   4096 Feb  4 15:38 journal
-rw-r-----  1 syslog    adm              49602 Feb 12 04:16 kern.log
drwxr-xr-x  2 landscape landscape         4096 Feb  4 15:40 landscape

I would use this when:
Investigating service failures or security issues.

---

## 6️⃣ /tmp

Description:
Stores temporary files. Usually cleared on reboot.

Command:
ls -l /tmp

Observed:
root@vagrant:/home/vagrant# ls -l /tmp
total 8
drwxr-xr-x 2 root root 4096 Feb 12 04:26 runbook-demo
drwx------ 3 root root 4096 Feb  4 15:38 systemd-private-9ca567bb19474a05a3780feca0d773a4-systemd-resolved.service-9L19Me

I would use this when:
Testing scripts or storing temporary outputs.

---

## 7️⃣ /bin

Description:
Contains essential system binaries (ls, cp, mv).

Command:
ls -l /bin | head

Observed:
root@vagrant:/home/vagrant# ls -l /bin | head
total 15352
-rwxr-xr-x 1 root root 1113504 Jun  6  2019 bash
-rwxr-xr-x 1 root root  716464 Mar 12  2018 btrfs
lrwxrwxrwx 1 root root       5 Mar 12  2018 btrfsck -> btrfs
-rwxr-xr-x 1 root root  375952 Mar 12  2018 btrfs-debug-tree

I would use this when:
Understanding where core commands are located.

---

## 8️⃣ /usr/bin

Description:
Contains user-level command binaries.

Command:
ls -l /usr/bin | head

Observed:
root@vagrant:/home/vagrant# ls -l /usr/bin | head
total 101228
-rwxr-xr-x 1 root   root       51384 Jan 18  2018 [
-rwxr-xr-x 1 root   root          96 Nov 27  2018 2to3-2.7
-rwxr-xr-x 1 root   root       22696 Sep 27  2018 aa-enabled
-rwxr-xr-x 1 root   root       22696 Sep 27  2018 aa-exec
-rwxr-xr-x 1 root   root       14608 Apr 28  2017 acpi_listen

I would use this when:
Checking installed applications.

---

## 9️⃣ /opt

Description:
Used for third-party or optional software.

Command:
ls -l /opt

Observed:
-rwxr-xr-x 1 root   root        2558 Feb 13  2018 apport-bug
root@vagrant:/home/vagrant# ls -l /opt
total 4
drwxr-xr-x 9 root root 4096 Aug 15  2019 VBoxGuestAdditions-6.0.10

I would use this when:
Managing manually installed applications.

---

# 🔎 Hands-On Tasks

## Find largest log files

du -sh /var/log/* 2>/dev/null | sort -h | tail -5

Observation:
root@vagrant:/home/vagrant# du -sh /var/log/* 2>/dev/null | sort -h | tail -5
28K     /var/log/apt
36K     /var/log/lastlog
52K     /var/log/kern.log
208K    /var/log/syslog
33M     /var/log/journal

---

## View hostname config

cat /etc/hostname

Observation:
root@vagrant:/home/vagrant# cat /etc/hostname
vagrant

---

## Check home directory

ls -la ~

Observation:
root@vagrant:/home/vagrant# ls -la ~
total 20
drwx------  2 root root 4096 Feb  8 03:53 .
drwxr-xr-x 24 root root 4096 Feb  4 15:39 ..
-rw-r--r--  1 root root 3106 Apr  9  2018 .bas

---
