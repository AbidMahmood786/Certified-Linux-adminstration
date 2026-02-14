# Chapter 4: Storage & LVM
CHAPTER 4 — Storage, Partitions & LVM (RHCSA‑Focused)
(Major topic – high chance of exam questions!)
1. RHCSA Objectives

Create partitions using fdisk and parted
Format filesystems (mkfs.xfs, mkfs.ext4)
Mount manually and via /etc/fstab
Manage LVM:

PV, VG, LV
Extend LV
Resize XFS


Configure swap (file or partition)


2. Essential Commands
lsblk
fdisk /dev/sdb
parted /dev/sdb mklabel gpt
mkfs.xfs /dev/sdb1
mount /dev/sdb1 /mnt
blkid

LVM:
pvcreate /dev/sdb1
vgcreate vgdata /dev/sdb1
lvcreate -L 2G -n lvdata vgdata
mkfs.xfs /dev/vgdata/lvdata
mount /dev/vgdata/lvdata /mnt/data
xfs_growfs /mnt/data

Swap:
mkswap /dev/sdb2
swapon /dev/sdb2
swapon --show


3. Fast Theory

XFS cannot shrink
LVM hierarchy: PV → VG → LV
/etc/fstab requires:

UUID
mountpoint
fs‑type
options


Wrong /etc/fstab entry can prevent boot

Fix by booting into emergency mode / rd.break




4. RHCSA Labs
Lab 1: Create + Format Partition
fdisk /dev/sdb
# create /dev/sdb1
mkfs.xfs /dev/sdb1
mount /dev/sdb1 /mnt

Verify:
df -h should show /mnt.

Lab 2: Create LVM
pvcreate /dev/sdb2
vgcreate vgdata /dev/sdb2
lvcreate -L 1G -n lvapps vgdata
mkfs.xfs /dev/vgdata/lvapps
mkdir /apps
mount /dev/vgdata/lvapps /apps


Lab 3: Extend LV
lvextend -L +500M /dev/vgdata/lvapps
xfs_growfs /apps


Lab 4: Permanent Mount
UUID=$(blkid -s UUID -o value /dev/vgdata/lvapps)
echo \"UUID=$UUID /apps xfs defaults 0 0\" >> /etc/fstab
mount -a


Lab 5: Create Swap
mkswap /dev/sdc1
swapon /dev/sdc1
5. Troubleshooting
IssueReasonFixLV won’t mountWrong UUIDCheck blkidSystem stuck at bootBad fstab entryRemove/repair via emergency modeLV won’t shrinkUsing XFSXFS cannot shrink
6. MCQs
Which command creates a PV?
A) pvcreate B) mkfs.xfs C) lvcreate D) vgcreate
Answer: A
Which FS cannot shrink?
A) ext4 B) xfs C) btrfs D) vfat
Answer: B
/etc/fstab incorrect entry causes:
A) Slow boot
B) No effect
C) Boot failure
D) SELinux error
Answer: C
To extend an XFS filesystem:
A) resize2fs
B) xfs_growfs
C) shrinkfs
D) fsresize
Answer: B


LV to filesystem order is:
A) LV → VG → PV
B) PV → LV → VG
C) PV → VG → LV
D) Mount → LV → VG
Answer: C


