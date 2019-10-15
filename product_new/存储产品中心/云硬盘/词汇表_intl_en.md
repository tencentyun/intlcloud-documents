## Cloud Block Storage 
Tencent Cloud CBS offers distributed block storage and freely configurable storage capacity that can be expanded on demand. Based on performance, products are divided into premium cloud storage, SSD cloud storage, and HDD cloud storage (the previous generation storage type).

### Non-elastic cloud disks
A non-elastic cloud disk is created along with the Cloud Virtual Machine (CVM) and its lifecycle follows that of the CVM. It does not support elastic mounting.

## Elastic cloud disks 
An elastic cloud disk has an independent lifecycle (billing cycle) and can be freely mounted or unmounted on different CVM instances in the same region and availability zone. It cannot be mounted simultaneously on multiple CVMs.

### Cloud disk snapshots 
A cloud disk snapshot is used to save a copy of the cloud disk at a point in time. You can use the snapshot to restore the cloud disk to the point in time when the snapshot was created.

### Full Snapshot
The first snapshot created for a disk, and all data on the disk is saved.

### Incremental Snapshot
After a full snapshot or the previous incremental snapshot has been taken, the subsequent snapshot only backs up files that have been added or modified relative to the previous snapshot. This is called an incremental snapshot.

### Snapshot Chain
Snapshot chain is a relationship chain made up of all the snapshots of the same disk. Each node represents one snapshot of the disk.

### Rollback
The restoration of a program or data to the previous correct state if a processing error occurs. Rollback types include program and data rollback.

### Random I/O
Random I/O means that the access addresses are not sequential, but randomly distributed in the address space of the LUN disk. Services that primarily generate random I/O include OLTP service, SQL, instant messaging services, etc.

### Sequential I/O
Sequential I/O means that read–write operations sequentially access data from adjacent addresses, one at a time by logic blocks. In sequential I/O access, disk seek time is greatly reduced because the read-write disk head barely needs to move to access the next block. Services such as data backups and log writing pipelines usually generate sequential I/O.

### IOPS
Input/Output per second (IOPS) refers to the number of reads (outputs) and writes (inputs) that take place in one second. This is an important indicator for measuring disk performance. IOPS indicates how many I/O requests the system can process in a given period of time, and the unit is the number of I/O requests processed per second. I/O requests are typically operation requests to read or write data. 
Traditional disks are essentially mechanical devices, such as FC, SAS and SATA disks, which typically spin at rates of 5400/7200/10000/15000rpm. The key factor that affects disks is the disk service time, or how long it takes for a disk to complete an I/O request. This time consists of three parts: seek time, rotational latency, and data transfer time.
Typically, a single HDD with 7,200 rpm provides 75-150 IOPS, and a single HDD with 15,000 rpm provides 175-210 IOPS. The specific value depends on factors such as access mode (sequential or random) and I/O size.

### Throughput
The amount of successfully transmitted data in a given unit of time over a network, device, port, virtual circuit or other devices.

### Striping
Striping is an automatic technique to balance I/O loads across multiple physical disks.

### Master Boot Record
Master Boot Record (MBR) is the sector that must be read first when a computer accesses the disk after being started. The MBR records information about the hard disk itself, and the size as well as location of all partitions on the disk. It is also an important entry for data information.

### GUID Partition Table
GUID Partition Table (GPT) is the partition format of a physical disk. It is part of the Extensible Firmware Interface (EFI) standard and is a replacement of the MBR partition table used by most existing disks.
