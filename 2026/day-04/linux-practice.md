List all running processes
ps -ef
Output (sample):

UID        PID  PPID  CMD
root         1     0  /sbin/init
ubuntu    1023     1  sshd: ubuntu@pts/0

--------------------------------------------------
Real-time process monitoring
top


Observed output:

CPU usage per process

Memory consumption

Load average
--------------------------------------------------
Find a specific process (ssh)
pgrep -a ssh


Output (sample):

1023 sshd: ubuntu@pts/0
--------------------------------------------------
Check SSH service status
systemctl status ssh


Output (sample):

Active: active (running)
Main PID: 1012 (sshd)
--------------------------------------------------
List active services
systemctl list-units --type=service --state=running


Output (sample):

ssh.service      loaded active running OpenBSD Secure Shell server
cron.service     loaded active running Regular background program processing daemon

--------------------------------------------------
 View logs for SSH service
journalctl -u ssh --no-pager | tail -n 10


Output (sample):

Accepted publickey for ubuntu from 10.0.0.5 port 54321


--------------------------------------------------


➡️ Thi
