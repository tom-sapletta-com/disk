# [Disk preparation on proxmox backup server](https://tom-sapletta-com.github.io/proxmox-disk/)

How to clean, format and prepare GPT array for proxmox

+ Try the steps, especially you got Issues during Proxmox Backup Server Initialize Disk with GPT 

## documents, sources

+ [How To Partition and Format Storage Devices in Linux - DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-partition-and-format-storage-devices-in-linux)
+ [How to Delete Partition in Linux](https://phoenixnap.com/kb/delete-partition-linux)
+ [How to Format Disk Partitions in Linux: ext4, NTFS and FAT32](https://phoenixnap.com/kb/linux-format-disk)
 
## info about disk

install
```
apt install hdparm
```

check:
```bash    
hdparm -I /dev/sdb  
```

out:
```
/dev/sdb:

ATA device, with non-removable media
        Model Number:       CT500P1SSD8                             
        Serial Number:      1913E1F4        
        Firmware Revision:  P3CR
Standards:
        Likely used: 1
Configuration:
        disk xfer rate <= 5Mbs
        data strobe offset option
        track offset option
        Logical         max     current
        cylinders       25601   0
        heads           0       0
        sectors/track   0       0
        --
        Logical/Physical Sector size:           512 bytes
        device size with M = 1024*1024:           0 MBytes
        device size with M = 1000*1000:           0 MBytes 
        cache/buffer size  = unknown
Capabilities:
        IORDY not likely
        Can perform double-word IO
        R/W multiple sector transfer: not supported
        DMA: not supported
        PIO: pio0
```



## parted

install
```
apt install parted
```

prepare:
```bash
parted /dev/sdb mklabel gpt
```

out:
```
Warning: The existing disk label on /dev/sdb will be destroyed and all data on this disk will be lost. Do you want to continue?
Yes/No? y                                                                 
Information: You may need to update /etc/fstab.
```


### GPT with proxmox tool
+ [Backup Storage — Proxmox Backup 3.0.1-1 documentation](https://pbs.proxmox.com/docs/storage.html)

To initialize a disk with a new GPT, use the initialize subcommand:

```bash
proxmox-backup-manager disk initialize sdb
```


### Delete Partitions with parted

Before deleting a partition, back up your data. 
All data is automatically deleted when a partition is deleted.

+ run the **d** command in the fdisk command-line utility.


![image](https://github.com/tom-sapletta-com/proxmox-disk/assets/5669657/f3f34a96-879b-4788-8631-98b549450216)


### Verify Partition Deletion

Reload the partition table to verify that the partition has been deleted. 

+ run the **p** command.

The terminal prints out the partition structure of the disk selected in Step 2.


### Save Changes and Quit

+ run the **w** command to write and save changes made to the disk.



## Formatting Disk Partition with ext4 File System

### Format a disk partition with the ext4 file system using the following command:

```bash
sudo mkfs -t ext4 /dev/sdb1
```

### Next, verify the file system change using the command:

```bash
lsblk -f
```


## Check disk performance

```bash
hdparm -Ttv /dev/sdb1
```

out:
```
/dev/sdb1:
 multcount     =  0 (off)
 readonly      =  0 (off)
 readahead     = 131064 (on)
 geometry      = 60801/255/63, sectors = 976771087, start = 2048
 Timing cached reads:   12072 MB in  2.00 seconds = 6041.48 MB/sec
 Timing buffered disk reads: 1214 MB in  3.04 seconds = 398.73 MB/sec
```

SPEED: **398.73 MB/sec**


## proxmox backup server


[/#pbsStorageAndDiskPanel](#pbsStorageAndDiskPanel)

![image](https://github.com/tom-sapletta-com/disk/assets/5669657/e56d1297-9dc4-43d7-80fc-837007d94312)



### create Directory

![image](https://github.com/tom-sapletta-com/disk/assets/5669657/015cede6-26e3-4946-a28c-dd6fb8df4fcd)


### Directory creating process

![image](https://github.com/tom-sapletta-com/disk/assets/5669657/730d2dcb-2e83-41cb-9474-71625a4021aa)


### Directory created

![image](https://github.com/tom-sapletta-com/disk/assets/5669657/28222c46-3b6b-4639-badb-464c8d8a7acd)


### Datastore created

![image](https://github.com/tom-sapletta-com/disk/assets/5669657/2b425743-a881-41cb-968b-3e66bec36072)




---
+ [edit](https://github.com/tom-sapletta-com/proxmox-disk/edit/main/README.md)
+ [https://github.com/tom-sapletta-com/proxmox-disk](https://github.com/tom-sapletta-com/proxmox-disk)

  
