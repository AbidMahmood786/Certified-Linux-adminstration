# Chapter 5: Users & Groups
✅ CHAPTER 5 — Users & Groups (RHCSA Exam–Focused)
1. RHCSA Objectives

Create, modify, delete users
Manage groups and supplementary groups
Configure password aging
Lock/unlock accounts
Understand /etc/passwd, /etc/shadow, /etc/group
Manage user defaults using /etc/login.defs and /etc/skel
Configure sudo access


2. Essential Commands
useradd john
passwd john
usermod -aG wheel john
userdel -r john
groupadd devs
gpasswd -a john devs
chage -l john
chage -M 90 -m 7 -W 14 john
passwd -l john
passwd -u john

System Files:
/etc/passwd
/etc/shadow
/etc/group
/etc/gshadow
/etc/login.defs
/etc/skel/

Sudo:
visudo


3. Fast Theory

/etc/passwd: user account info
/etc/shadow: password hashes + aging
/etc/group: group memberships
useradd uses defaults from /etc/login.defs
/etc/skel provides default files for new users
Password aging ensures security compliance
Sudo rules must be edited using visudo (avoids syntax errors)


4. RHCSA Labs
Lab 1 — Create User with Password
useradd sara
passwd sara

Validate:
Check /etc/passwd for entry.

Lab 2 — Add User to a Secondary Group
groupadd project
usermod -aG project sara

Validate:
id sara

Lab 3 — Configure Password Aging
chage -M 60 -m 7 -W 10 sara


Lab 4 — Lock and Unlock User
passwd -l sara   # lock
passwd -u sara   # unlock


Lab 5 — Sudo Access
Add user in /etc/sudoers:
visudo

Add line:
sara ALL=(ALL) ALL


5. Troubleshooting

























IssueReasonFixUser not in groupForgot -a with -Gusermod -aG group user"Permission denied" for sudoUser not in sudoers/wheelAdd to wheel groupAccount locked/etc/shadow has !passwd -u user

6. MCQs


Which file stores password hashes?
A) /etc/passwd B) /etc/shadow C) /etc/group D) /etc/secure
Answer: B


Add user to group without removing existing groups:
A) usermod -G grp user
B) usermod -aG grp user
C) groupadd user grp
D) addgroup user grp
Answer: B


Default files for new users come from:
A) /etc/conf
B) /home/default
C) /etc/skel
D) /var/lib/user
Answer: C


Which command locks a user account?
A) chage -l
B) passwd -l
C) usermod -L
D) Both B & C
Answer: D


Where is sudo configuration stored?
A) /etc/sudo
B) /etc/groups
C) /etc/sudoers
D) /etc/sudoconf
Answer: C

