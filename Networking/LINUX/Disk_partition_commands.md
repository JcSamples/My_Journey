
# Disk and Partition Management Commands

## 1. **Entering the Disk Utility**

```bash
sudo enter_disk /dev/sdb
```
*This command is used to enter the disk utility for managing partitions.*

---

## 2. **Wipe Partitions**

```bash
sudo wipe_partitions -a /dev/sdb
```

```bash
sudo wipe_partitions -g /dev/sdb
```
*These commands are used to remove all existing partitions from the disk.*

---

## 3. **Disk Partitioning Commands**

### Entering the Disk Utility

```bash
sudo enter_disk /dev/sdb
```
*This command starts the disk utility for the specified disk.*

### Adding a New Partition

```bash
n
```
*This command is used within the disk utility to add a new partition.*

### Verify Partition for Errors

```bash
v
```
*This command is used to verify that the partition is free of errors.*

### Create a New Partition Table

```bash
o
```
*This command is used to create a new partition table.*

---

## 4. **GNU Parted Tool**

*GNU Parted is another tool available for creating and resizing partitions on a hard drive. It includes both a command-line tool (`parted`) and a graphical interface (`gparted`).*

### 4.1 **Resize a Partition (Non-Destructive)**

*The GNU Parted tool can non-destructively resize a partition as well as the file system defined on it.*

### 4.2 **Using Parted**

*Parted can be used in two ways:*

1. **Command-Line Mode**
2. **Interactive Mode**

*When using `parted` in either mode, a device must be specified:*

```bash
parted [options] [DEVICE [command [options …]] …]
```

### Command-Line Example:

```bash
sudo parted /dev/sdb print
```
*This command is used to display information about existing partitions on the disk.*

### Create a Partition Table

```bash
sudo parted /dev/sdb
```
*This command initiates `parted` to create a partition table on the specified disk.*

### Create a Primary Partition

```bash
sudo parted /dev/sdb mkpart primary 0% 50%
```
*This command creates a primary partition occupying the first 50% of the disk.*

*Note: You must always specify the type of partition you want (GPT or MBR).*

---

## 5. **Interactive Mode in GNU Parted**

### Start Interactive Mode

```bash
parted /dev/sdb
```
*This command starts `parted` in interactive mode.*

### Select Another Device

```bash
select /dev/sdb
```
*This command selects a different device in interactive mode.*

### Format Partition to ext4

```bash
mkfs.ext4 /dev/sdb1
```
*This command formats the partition as ext4.*

### Verify Partition

```bash
sudo parted /dev/sdb1 print
```
*This command verifies the partition.*

---

## 6. **Resizing a Partition**

### Resize Command

```bash
resizepart
```
*This command is used to resize a partition.*

### Example Workflow:

1. **Start parted**:

```bash
parted /dev/sdb
```

2. **Print Current Partitions**:

```bash
print
```

3. **Resize a Partition**:

```bash
resizepart
```
*You will be prompted to specify the partition number and the new size.*

4. **Print to Verify Changes**:

```bash
print
```

---

## 7. **Delete a Partition**

### Remove Partition Command

```bash
rm <partition_number>
```
*This command deletes the specified partition.*

---

## 8. **Recover a Partition**

### Rescue Command

```bash
rescue
```
*This command attempts to recover a lost partition by specifying the start and end sectors.*

---

## 9. **Change Partition Flags**

*Flags indicate certain properties or active features of a partition. Flags can be toggled on or off. If a flag is not visible, it is inactive or nonexistent.*

---

## 10. **Creating a Swap Partition**

### Create Swap Partition of Type 82

```bash
mkswap /dev/sda3
```
*This command converts the partition into swap space.*

### Enable Swap Space

```bash
swapon /dev/sda3
```
*This command enables the partition as the current swap space.*

### Display Current Swap Usage

```bash
swapon -s
```
*This command displays the swap space currently in use.*

---

## 11. **Create a Swap File**

### Create a Large Swap File

```bash
dd if=/dev/zero of=/var/extraswap bs=1M count=100
```
*This command uses `dd` to create a large swap file.*

### Convert File to Swap Space

```bash
mkswap /var/extraswap
```
*This command converts the file into swap space.*

### Enable the Swap File

```bash
swapon /var/extraswap
```
*This command enables the file as swap space.*

---

## 12. **Swappiness Configuration**

*Swappiness is a Linux kernel parameter that defines how often the system uses swap space. The value can range from 0 to 100, with a default of 60. A lower value makes the kernel less likely to use swap, while a higher value increases swap usage.*

### Check Current Swappiness Value

```bash
cat /proc/sys/vm/swappiness
```
*This command checks the current swappiness value.*

### Temporarily Change Swappiness Value

```bash
sudo sysctl vm.swappiness=10
```
*This command temporarily changes the swappiness value.*

### Permanently Change Swappiness Value

1. **Edit the Configuration File**:

```bash
sudo nano /etc/sysctl.conf
```

2. **Add the Following Line**:

```bash
vm.swappiness=<value>
```
*This line sets the swappiness value permanently.*

### Disable Swap

```bash
sudo swapoff -v [file/partition]
```
*This command disables swap on the specified file or partition, allowing you to remove it afterward.*
