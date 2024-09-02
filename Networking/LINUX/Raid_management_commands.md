
# RAID Management Commands in Linux

This guide provides commands for managing RAID arrays on a Linux system, including creating, formatting, mounting, and expanding RAID arrays. The examples use NVMe drives, but the principles apply to other drive types as well.

## 1. Install and Configure NVMe Disks

**Objective:** Install 4 NVMe disks for RAID configuration.

## 2. Create RAID Arrays in Linux

### 2.1 List Available Disks

Use the following command to list all available disks (excluding loop devices) and their mount points:
```bash
lsblk -e7 -o NAME,SIZE,FSTYPE,TYPE,MOUNTPOINT
```

### 2.2 View Existing RAID Arrays

Check the status and availability of existing RAID arrays:
```bash
cat /proc/mdstat
```

### 2.3 Create a RAID 0 Array

Create a RAID 0 array with two NVMe disks:
```bash
mdadm --create /dev/md0 --level=0 --raid-devices=2 /dev/nvme0n1 /dev/nvme0n2
```

**Note:** Chunks refer to the size of the blocks that are striped across the RAID devices. The default value can be adjusted with the `--chunk` option.

### 2.4 Format the RAID Array

Format the newly created RAID array with the ext4 filesystem:
```bash
mkfs.ext4 -F /dev/md0
```

### 2.5 Mount the RAID Array

Mount the RAID array to a specific directory:
```bash
mount /dev/md0 /mnt/md0
```

### 2.6 Test the RAID Setup

Create a test file to ensure the RAID is functioning:
```bash
touch /mnt/md0/raid.txt
```

## 3. Configure System to Automatically Mount RAID on Boot

### 3.1 Generate mdadm Configuration

Navigate to the mdadm directory and configure the array to auto-assemble on boot:
```bash
cd /etc/mdadm
mdadm --detail --scan | tee -a /etc/mdadm/mdadm.conf
```

### 3.2 Update fstab

Add the RAID array to `/etc/fstab` for automatic mounting:
```bash
echo '/dev/md0 /mnt/md0 ext4 defaults,nofail,discard 0 0' | tee -a /etc/fstab
```

### 3.3 Update initramfs

Update the initial RAM filesystem to include the RAID configuration:
```bash
update-initramfs -u
```

## 4. Create a RAID 1 Array

### 4.1 Create the RAID 1 Array

Use the following command to create a RAID 1 array:
```bash
mdadm --create /dev/md1 --level=1 --raid-devices=2 /dev/nvme0n3 /dev/nvme0n4
```

### 4.2 Repeat Formatting and Mounting Steps

Repeat the steps to format and mount the RAID 1 array as shown in sections 2.4 and 2.5.

## 5. Stop and Remove RAID Arrays

### 5.1 Unmount and Stop the RAID Device

Unmount the device and stop the RAID array:
```bash
umount /dev/md0
mdadm --stop /dev/md0
```

### 5.2 Check for Mount Points

Ensure that the device is no longer mounted and check the disk status:
```bash
lsblk -e7 -o NAME,SIZE,FSTYPE,MOUNTPOINT
```

### 5.3 Remove Disks from RAID

To remove a disk from the RAID array, use:
```bash
mdadm --zero-superblock /dev/nvme0n1
mdadm --zero-superblock /dev/nvme0n2
```

### 5.4 Comment Out fstab and mdadm.conf Entries

If you have removed the RAID array, comment out the relevant entries in `/etc/fstab` and `/etc/mdadm/mdadm.conf`.

### 5.5 Update initramfs Again

After making changes, update the initramfs:
```bash
update-initramfs -u
```

## 6. Create a RAID 10 Array

### 6.1 Create the RAID 10 Array

To create a RAID 10 array, you can use:
```bash
mdadm --create /dev/md10 --level=10 --raid-devices=4 /dev/nvme0n1 /dev/nvme0n2 /dev/nvme0n3 /dev/nvme0n4
```

### 6.2 View RAID Information

Check detailed information about the RAID array:
```bash
mdadm -D /dev/md10
mdadm -Db /dev/md10
mdadm -Q /dev/md10
```

## 7. Add a Disk to an Existing RAID Array

### 7.1 Adding a Disk to RAID 5

To add an additional disk to a RAID 5 array:
```bash
mdadm /dev/md5 --add /dev/nvme0n4
```

### 7.2 Update mdadm Configuration

After adding a disk, update the mdadm configuration:
```bash
mdadm --detail --brief /dev/md127 | tee -a /etc/mdadm/mdadm.conf
```

### 7.3 Mark a Disk as Failed

To mark a disk as failed in a RAID array:
```bash
mdadm /dev/md5 --fail /dev/nvme0n4
```

## 8. Expand RAID Arrays

### 8.1 Grow a RAID 5 or 6 Array

To grow a RAID 5 or RAID 6 array, use:
```bash
mdadm --grow --raid-devices=4 --backup-file=/root/md127-grow.bak /dev/md127
```

### 8.2 Add a Disk and Grow a RAID 10 Array

To add a disk to a RAID 10 array and grow it:
```bash
mdadm --grow /dev/md10 --raid-devices=3 --add /dev/nvme0n*
```

---

For more detailed instructions, refer to the official documentation or additional resources like [this video](https://www.youtube.com/watch?v=boqC9QenshY).
