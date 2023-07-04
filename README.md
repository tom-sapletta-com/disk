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
