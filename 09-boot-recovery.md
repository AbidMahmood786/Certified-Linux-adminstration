# Chapter 9: Boot & Recovery

✅ CHAPTER 9 — Boot, GRUB2 & Recovery (RHCSA Exam‑Focused)
1. RHCSA Objectives

Understand Linux boot sequence
Work with GRUB2 bootloader
Reset root password using rd.break
Boot into rescue/emergency mode
Manage kernels
Regenerate GRUB config


2. Essential Commands
grub2-mkconfig -o /boot/grub2/grub.cfg
grub2-set-default <entry>
grubby --default-kernel
grubby --set-default /boot/vmlinuz-<version>
rpm -qa kernel
reboot

Reset Root Password
(Exam Critical)
rd.break
mount -o remount,rw /sysroot
chroot /sysroot
passwd root
touch /.autorelabel
exit
exit

Boot Targets
systemctl rescue
systemctl emergency


3. Fast Theory

Boot sequence:
BIOS/UEFI → GRUB2 → Kernel → systemd → targets/services
GRUB2 config file:
/boot/grub2/grub.cfg (Do NOT edit manually)
Modify default kernel using grubby
rd.break drops system into initramfs debug shell before root mount
/.autorelabel triggers SELinux relabeling on next boot
Rescue mode mounts system read‑write with limited services
Emergency mode mounts / read‑only with no services


4. RHCSA Labs
Lab 1 — Regenerate GRUB2 Configuration
grub2-mkconfig -o /boot/grub2/grub.cfg


Lab 2 — Change Default Kernel
grubby --set-default /boot/vmlinuz-$(ls /boot | grep vmlinuz | head -1)
grubby --default-kernel


Lab 3 — Boot into Rescue Mode
systemctl rescue


Lab 4 — Reset Root Password

At GRUB menu → press e
Append:
rd.break


Boot with Ctrl+X
Run:
mount -o remount,rw /sysroot
chroot /sysroot
passwd root
touch /.autorelabel
exit
exit




5. Troubleshooting

























IssueReasonFixGRUB doesn’t show menuFastboot enabledPress ESC at bootBoot failure after fstab editWrong UUID/formatBoot with rd.break, fix fstabSELinux relabel takes longLarge filesystemWait — required after passwd reset

6. MCQs


GRUB2 config file is located at:
A) /etc/grub.cfg B) /boot/grub2/grub.cfg C) /etc/default/grub D) /boot/kernel.cfg
Answer: B


Command to regenerate GRUB config:
A) grub-update B) grub-make C) grub2-mkconfig D) grub-fix
Answer: C


rd.break stops boot:
A) After systemd starts
B) Before root FS mounts
C) After boot completes
D) At login screen
Answer: B


/.autorelabel is used for:
A) Kernel update
B) SELinux relabel on reboot
C) GRUB recovery
D) Reset network
Answer: B


Rescue mode command:
A) systemctl fix
B) systemctl rescue
C) systemctl emergency
D) ctl-rescue
Answer: B


