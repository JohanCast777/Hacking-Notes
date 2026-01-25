
## Types of file system

| **File System** | **Primary OS**                        | **Journaling** | **Main Usage**                             | **Notable Features / Characteristics**                                                       |
| --------------- | ------------------------------------- | -------------- | ------------------------------------------ | -------------------------------------------------------------------------------------------- |
| **ext2**        | Linux                                 | ❌ No           | Lightweight setups, removable drives (USB) | Simple and fast, no journaling (less resilient to crashes), minimal overhead                 |
| **ext3**        | Linux                                 | ✅ Yes          | General-purpose Linux storage              | Backward-compatible with ext2, adds journaling for better crash recovery                     |
| **ext4**        | Linux                                 | ✅ Yes          | Default modern Linux file system           | Efficient journaling, supports very large files and volumes, reliable and widely used        |
| **Btrfs**       | Linux                                 | ✅ Yes          | Advanced storage management                | Supports snapshots, subvolumes, checksumming, and dynamic resizing; great for data integrity |
| **XFS**         | Linux                                 | ✅ Yes          | High-performance environments              | Excellent for large files and high I/O workloads (servers, multimedia, databases)            |
| **NTFS**        | Windows (and Linux for compatibility) | ✅ Yes          | Dual-boot systems, external drives         | Proprietary Microsoft file system; ensures cross-compatibility between Linux and Windows     |

## Inodes

![[Pasted image 20260117152428.png|1000]]


## Disk Management

Shows the `📦` devices or (partitions), hardware view.

```
lsblk
```

```
sudo fdisk -l
```

Check the file (Permissions)
```
ll /dev/nvme0n1
```

## Mounting

Shows all the currectly mounted files
```
mount
```

Mount a disk
```
sudo mount /dev/sdb1 ~/USBtest/
```

Umount a disk
```
sudo umount /dev/sdb1
```

Mount main file to set booting options
```
nano /etc/fstab
```

Create a new partition table
```
sudo fdisk /dev/sdb
```

This are the possible commands
![[Pasted image 20260117224045.png]]

|Scheme|Year Created|Company|Primary Use|
|---|---|---|---|
|MBR|1983|IBM|PC DOS/Windows systems|
|Sun|~1983-1985|Sun Microsystems|SunOS/Solaris SPARC|
|SGI|1988|Silicon Graphics|IRIX on MIPS|
|GPT|~1997-1999|Intel|UEFI systems, modern OSes|


To take off the USB

```
sudo umount -l /dev/sdb1
```
```
sync
```
```
sudo eject /dev/sdb
```
```
lsblk | grep sdb
```

## Format a the disk

Format the disk an set an specific file system
```
sudo mkfs.exfat /dev/sdb1
```

With this command and clicking tap we can check some of the availables file systems 
![[Pasted image 20260124203038.png]]

Show mounted file systems 
```
df -h
```


==COMPLETE THIS SETION AND USE THE OTHER TESTING PC PLS==


https://www.youtube.com/watch?v=2Z6ouBYfZr8