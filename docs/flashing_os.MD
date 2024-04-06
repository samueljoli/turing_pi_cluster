# Installing Alpine on RPI 4 (macOS arm 🦾)

## Overview

**What you'll be doing**

- preparing your SD card(s)
- downloading `Alpine Linux` and writing it to the SD card
- configuring boot options

**Why Alpine Linux?**

### Step 1
**List Available Disks:**
```bash
diskutil list
```
The SD card should have the `(external, physical)` markers:
```
/dev/disk6 (disk image):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        +252.8 MB   disk6
   1:                  Apple_HFS ⁨balenaEtcher 1.18.11⁩    252.8 MB   disk6s1
```

**Partitioning the SD Card:**
> [!NOTE]
> Raspberry Pi's have a special boot procedure that uses a FAT partition [^1] and the GPU.

Create a single partition formatted with a FAT32 file system and label it "ALPINE", and allocate 100% of the disk's available space to this partition.
```bash
diskutil partitionDisk /dev/disk4 MBR FAT32 ALPINE 100%
```

[^1]: A FAT (File Allocation Table) partition is a type of file system used for storing data on storage devices like hard drives, SSDs, and SD cards.
The FAT file system is one of the oldest and most widely compatible file systems, making it a common choice for boot partitions and removable storage.
There are several versions of FAT, with FAT32 being the most common for larger storage devices due to its support for larger file sizes and partitions compared to its predecessors, FAT12 and FAT16.
