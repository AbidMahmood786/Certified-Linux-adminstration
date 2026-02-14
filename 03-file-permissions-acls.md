# Chapter 3: File Permissions & ACLs
CHAPTER 3 — File Permissions & ACLs (RHCSA‑Focused, Concise)
1. RHCSA Objectives

Manage permissions using chmod, chown, chgrp
Understand permission classes: user/group/other
Set special permissions: SUID, SGID, Sticky Bit
Configure ACLs using setfacl, getfacl
Diagnose access problems


2. Essential Commands
chmod 755 file
chmod u+x,g-w,o=r file
chown user:group file
chgrp group file
ls -l
getfacl file
setfacl -m u:john:rwx file
setfacl -x u:john file
setfacl -m g:developers:rw /project
setfacl -k file    # remove default ACLs

Special Bits:
chmod 4755 file   # SUID
chmod 2755 dir    # SGID
chmod 1755 dir    # Sticky bit


3. Fast Theory


Normal permissions:

r = read
w = write
x = execute (or access directory)



Permission order:
user → group → other


SUID:

Executed as owner
Used by /usr/bin/passwd



SGID:

Files inherit the directory’s group



Sticky bit:

Only owner can delete files in directory
Used in /tmp



ACLs provide fine‑grained permissions beyond owner/group/other.



4. RHCSA Labs
Lab 1 — Set File Permissions
touch file1
chmod 640 file1
ls -l file1

Verify:
Permissions should be rw-r-----.

Lab 2 — Configure ACL for a User
setfacl -m u:john:rw file1
getfacl file1

Verify:
You should see user:john:rw-.

Lab 3 — SGID Directory for Project Work
mkdir /project
chgrp developers /project
chmod 2775 /project

Verify:
All files created inside inherit group developers.

Lab 4 — Sticky Bit
mkdir /shared
chmod 1777 /shared


5. Troubleshooting

























IssueCauseFixUser cannot writeWrong group or missing ACLgetfacl, chown, setfaclUnexpected denyACL overrides unix permsCheck mask in ACLUsers deleting others’ filesMissing sticky bitchmod 1777 dir

6. MCQs


Which permission bit prevents users from deleting others’ files?
A) SUID B) SGID C) Sticky Bit D) Mask
Answer: C


To give user john rw access using ACL:
A) chown john file
B) chmod 777 file
C) setfacl -m u:john:rw file
D) chgrp john file
Answer: C


SGID on a directory means:
A) directory executable by group
B) files inherit group ownership
C) users run as root
D) all users can delete
Answer: B


View ACLs:
A) ls
B) cat
C) getfacl
D) id
Answer: C


Permission 755 means:
A) rwxrwxrwx
B) rw-r--r--
C) rwxr-xr-x
D) r--r--r--
Answer: C




