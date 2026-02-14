# Chapter 1: Core Linux Concepts
1. RHCSA Objectives

Understand Linux directory hierarchy
Use man, info, and built‑in help
Locate configuration files under /etc
Identify log files under /var/log
Understand virtual filesystems (/proc, /sys)


2. Essential Commands
man <cmd>
info <cmd>
whatis <cmd>
apropos <term>
ls /etc
ls /var/log
uname -r
hostnamectl


3. Fast Theory

FHS (Filesystem Hierarchy Standard) defines directory purposes:

/ → Root of entire filesystem
/etc → System configuration
/var → Logs, spools, caches
/home → User data
/bin, /sbin → Essential binaries
/usr/bin → Most installed commands
/proc → Kernel and process info (virtual FS)
/sys → Kernel hardware interfaces (virtual FS)


Help systems:

man uses sections (1=commands, 5=config, 8=admin)
info for GNU tools
--help for command summaries

4. RHCSA Labs
Lab 1: Explore Linux directories
Objective: Identify key locations required in the exam.
Steps:
ls /
ls /etc
ls /var/log
ls /proc

Validate:

Confirm /etc/passwd exists
Confirm /var/log/messages or /var/log/journal exists


Lab 2: Use help systems
Objective: Learn where command documentation lives.
Steps:
man ls
info coreutils
ls --help
apropos password
man 5 passwd

Validate:

Check that man 5 passwd shows file format details


5. Troubleshooting


ProblemCauseFixman pages missingman-db not installeddnf install man-dbConfusing directory contentsNot using long listingls -lWrong man sectionDid not specify sectionman 5 passwd
6. MCQs

Which directory stores system configuration files?
A) /usr/bin B) /etc C) /opt D) /var  Answer: B


Which command searches the man database?
A) man -k B) whatis C) help D) ls  Answer: A


/proc is:
A) Virtual FS B) Boot files C) Logs D) Config files  Answer: A


man 5 fstab opens:
A) Command usage B) Config file format C) Kernel docs D) Admin commands  Answer: B


/var/log contains:
A) User data B) Bootloader C) Log files D) Commands  Answer: C
