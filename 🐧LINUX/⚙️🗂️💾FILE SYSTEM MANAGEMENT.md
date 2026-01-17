
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


## Management

