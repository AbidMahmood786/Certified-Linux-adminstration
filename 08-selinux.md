# Chapter 8: SELinux
CHAPTER 8 — SELinux (RHCSA Exam‑Focused)
(One of the MOST tested topics in RHCSA)
1. RHCSA Objectives

Check SELinux mode and status
Change mode (permanent and temporary)
Manage SELinux file contexts
Use semanage fcontext
Restore contexts using restorecon
Enable SELinux booleans
Diagnose and fix SELinux‑related service failures


2. Essential Commands
Check SELinux Status
sestatus
getenforce
setenforce 0     # permissive
setenforce 1     # enforcing

File Contexts
ls -Z
semanage fcontext -a -t httpd_sys_content_t '/web(/.*)?'
restorecon -Rv /web

Booleans
getsebool -a
setsebool -P httpd_can_network_connect on

SELinux Logs
ausearch -m avc -ts recent
journalctl -t setroubleshoot


3. Fast Theory

SELinux modes:

Enforcing → policy applied
Permissive → logs only
Disabled → no SELinux


Context components:
user:role:type:level


Type Enforcement (TE) is the core of SELinux.
Web content must use:

httpd_sys_content_t


Services blocked from network access may require booleans such as:

httpd_can_network_connect
httpd_can_network_relay




4. RHCSA Labs
Lab 1 — Check and Change Mode
sestatus
setenforce 0
setenforce 1


Lab 2 — Fix Wrong Context on Web Directory
mkdir -p /web
echo "Hello" > /web/index.html
ls -Z /web
semanage fcontext -a -t httpd_sys_content_t "/web(/.*)?"
restorecon -Rv /web


Lab 3 — Enable Boolean for HTTP Network Access
setsebool -P httpd_can_network_connect on
getsebool httpd_can_network_connect


Lab 4 — Investigate SELinux Denials
ausearch -m avc
journalctl -t setroubleshoot


5. Troubleshooting


IssueReasonFixApache cannot read custom directoryWrong SELinux contextApply semanage fcontext + restoreconApp cannot make network requestsBoolean disabledsetsebool -P httpd_can_network_connect onDenials hard to understandNo logs visibleUse ausearch -m avc

6. MCQs


Check SELinux mode:
A) getmode B) selinuxctl C) sestatus D) ctxmode
Answer: C


Temporary permissive mode:
A) setenforce permissive
B) setenforce 0
C) selinux 0
D) disableenforce
Answer: B


Wrong file context fix:
A) fixctx
B) selinux-fix
C) restorecon
D) semanage fix
Answer: C


Set permanent context for directory:
A) restorecon -p
B) semanage fcontext
C) chcon -R
D) chmod --selinux
Answer: B


Allow Apache to connect outwards:
A) httpd_enable_connect
B) httpd_can_net
C) httpd_can_network_connect
D) web_connect
Answer: C


