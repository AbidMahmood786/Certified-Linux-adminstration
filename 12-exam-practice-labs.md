# Chapter 12: Exam Practice Labs

✅ CHAPTER 12 — RHCSA Practice Labs (Exam‑Level Tasks)
These are realistic RHCSA-style tasks, designed to match Red Hat exam patterns.

🔥 SECTION A — STORAGE & LVM LABS
Lab A1 — Create LVM and Mount Permanently

Create partition /dev/sdb1
Convert to PV:
pvcreate /dev/sdb1


Create VG:
vgcreate vgdata /dev/sdb1


Create LV:
lvcreate -L 3G -n lvfiles vgdata


Format:
mkfs.xfs /dev/vgdata/lvfiles


Mount at /files


Lab A2 — Extend LV
lvextend -L +1G /dev/vgdata/lvfiles
xfs_growfs /files


🔥 SECTION B — USER & GROUP LABS
Lab B1 — Create Users with Expiration
useradd -e 2026-12-31 bob
passwd bob


Lab B2 — Add Users to Project Group
groupadd project
usermod -aG project bob


🔥 SECTION C — NETWORKING LABS
Lab C1 — Configure Static IP
nmcli con mod eth0 ipv4.addresses 192.168.10.50/24
nmcli con mod eth0 ipv4.gateway 192.168.10.1
nmcli con mod eth0 ipv4.dns 8.8.8.8
nmcli con mod eth0 ipv4.method manual
nmcli con up eth0


Lab C2 — Open Firewall Port
firewall-cmd --add-port=8080/tcp --permanent
firewall-cmd --reload


🔥 SECTION D — SELinux LABS
Lab D1 — Fix SELinux for Custom Web Directory
semanage fcontext -a -t httpd_sys_content_t "/web(/.*)?"
restorecon -Rv /web


Lab D2 — Allow Apache Outbound Connections
setsebool -P httpd_can_network_connect on


🔥 SECTION E — SYSTEMD LABS
Lab E1 — Enable Service
systemctl enable --now httpd


Lab E2 — Create systemd Unit for Podman Container
podman generate systemd --name web --files
cp container-web.service ~/.config/systemd/user/
systemctl --user daemon-reload
systemctl --user enable --now container-web.service

🔥 SECTION F — BOOT & RECOVERY LABS
Lab F1 — Reset Root Password
(Exam-critical)

Boot → GRUB → press e
Add: rd.break
Boot
Run:
mount -o remount,rw /sysroot
chroot /sysroot
passwd root
touch /.autorelabel
exit
exit

Lab F2 — Fix Broken fstab Entry

Boot with rd.break
Mount root
Edit /etc/fstab
Reboot
