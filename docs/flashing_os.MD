# Installing Alpine on Raspberry Pi 4

## Overview

This guide assumes you're on `macOS` (arm 🦾)

**What you'll be doing**

1. preparing your SD card(s)
2. downloading `Alpine Linux` [^1] and writing it to the SD card
3. configuring boot options


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
> Raspberry Pi's have a special boot procedure that uses a FAT partition [^2] and the GPU [^3].

Create a single partition formatted with a FAT32 file system of type Master Boot Record  and label it "ALPINE", and allocate 100% of the disk's available space to this partition.
```bash
diskutil partitionDisk /dev/disk4 MBR FAT32 ALPINE 100%
```

### Step 2

**Download `Alpine Linux` and write to SD card:**

```bash
curl -L http://dl-cdn.alpinelinux.org/alpine/v3.12/releases/aarch64/alpine-rpi-3.12.1-aarch64.tar.gz | tar -xz -C /Volumes/ALP/
```

[^1]: Alpine Linux is a Linux distribution designed to be small, simple, and secure. It uses musl, BusyBox, and OpenRC instead of the more commonly used glibc, GNU Core Utilities, and systemd. I decided on this distroy to reduce image size and improve startup times.

[^2]: A FAT (File Allocation Table) partition is a type of file system used for storing data on storage devices like hard drives, SSDs, and SD cards.
The FAT file system is one of the oldest and most widely compatible file systems, making it a common choice for boot partitions and removable storage.
There are several versions of FAT, with FAT32 being the most common for larger storage devices due to its support for larger file sizes and partitions compared to its predecessors, FAT12 and FAT16.

[^3]: The Raspberry Pi boot process begins with the GPU (Graphics Processing Unit) rather than the CPU (Central Processing Unit) because the GPU is responsible for initializing and configuring the system before the CPU takes over. The GPU is also responsible for loading the firmware and bootloader, which are then used to boot the operating system and hand over control to the CPU. This allows the Raspberry Pi to boot quickly and efficiently, as the GPU can perform many tasks in parallel while the CPU is still starting up
