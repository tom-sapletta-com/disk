# disk
How to clean, format and prepare GPT array for proxmox


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



## with parted

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



## proxmox backup server


[/#pbsStorageAndDiskPanel](#pbsStorageAndDiskPanel)

![image](https://github.com/tom-sapletta-com/disk/assets/5669657/e56d1297-9dc4-43d7-80fc-837007d94312)



### create Directory

![image](https://github.com/tom-sapletta-com/disk/assets/5669657/015cede6-26e3-4946-a28c-dd6fb8df4fcd)


### process

![image](https://github.com/tom-sapletta-com/disk/assets/5669657/730d2dcb-2e83-41cb-9474-71625a4021aa)


### created disk

![image](https://github.com/tom-sapletta-com/disk/assets/5669657/28222c46-3b6b-4639-badb-464c8d8a7acd)
