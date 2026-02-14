# Chapter 7: Networking & Firewalld
✅ CHAPTER 6 — Systemd & Service Management (RHCSA‑Focused)
1. RHCSA Objectives

Control system services using systemctl
Understand systemd unit types
Manage targets (multi‑user, graphical)
Analyze logs using journalctl
Enable/disable services
Mask/unmask services
Create or edit simple unit files


2. Essential Commands
systemctl start httpd
systemctl stop firewalld
systemctl restart sshd
systemctl status crond
systemctl enable --now cockpit.socket
systemctl disable cups
systemctl mask bluetooth
systemctl unmask bluetooth

Targets:
systemctl get-default
systemctl set-default multi-user.target

Logs:
journalctl -u httpd
journalctl -u sshd -xe
journalctl --since "10 min ago"


3. Fast Theory


systemd manages:

Services
Sockets
Mounts
Targets



Common Unit Types:

.service
.socket
.mount
.target



systemctl enable creates symlink for auto‑start


systemctl mask prevents manual and automatic start


Logs are stored in binary format by journald

Viewed using journalctl




4. RHCSA Labs
Lab 1 — Start/Stop Services
systemctl start httpd
systemctl status httpd
systemctl stop httpd


Lab 2 — Enable Service on Boot
systemctl enable --now sshd


Lab 3 — Check and Change Default Target
systemctl get-default
systemctl set-default multi-user.target


Lab 4 — Service Logs
journalctl -u sshd
journalctl -xe


Lab 5 — Mask a Service
systemctl mask cups
systemctl unmask cups


5. Troubleshooting

























IssueReasonFixService won’t startBad config filejournalctl -u serviceFails at bootMissing enablesystemctl enable serviceService starts unexpectedlyEnabled or socket activatedsystemctl disable, check .socket

6. MCQs


To start a service immediately:
A) service start service
B) sysctl service start
C) systemctl start service
D) initctl start
Answer: C


To check logs for sshd:
A) logs sshd
B) journalctl -u sshd
C) systemctl log sshd
D) view ssh logs
Answer: B


Masking a service:
A) Stops it
B) Prevents all starting methods
C) Deletes it
D) Hides config
Answer: B


Change default target:
A) systemctl target set
B) systemctl set-default
C) systemctl change target
D) initctl default
Answer: B


Which unit type describes system services?
A) .mount
B) .socket
C) .service
D) .target
Answer: C


