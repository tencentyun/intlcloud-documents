

### Elastic cloud disks

An elastic cloud disk has an independent lifecycle (billing cycle) and can be freely mounted and unmounted to different CVM instances in the same availability zone of one region. However, it cannot be mounted simultaneously on multiple CVMs.



### Non-elastic cloud disks

A non-elastic cloud disk is created along with a Cloud Virtual Machine (CVM) and has the same lifecycle as that of the CVM. It does not support elastic mounting.



### GPT

See [GPT](https://intl.cloud.tencent.com/document/product/362/18555).



### Rollback

A rollback is to restore a program or data to the last correct status if a processing error occurs. There are two kinds of rollback, program and data rollback.



### IOPS

Input/Output Per Second (IOPS) refers to the number of reads (outputs) and writes (inputs) in one second. This is an important indicator for measuring disk performance. IOPS indicates how many I/O requests the system can process in a given period of time (generally in a second). I/O requests are typically requests to read or write data.
Traditional disks are essentially mechanical devices, such as FC, SAS and SATA disks, which typically spin at rates of 5,400/7,200/10,000/15,000 rpm. The key factor that affects disks is the disk service time, or how long it takes for a disk to complete an I/O request. This time consists of three parts: seek time, rotational latency, and data transfer time.
Typically, a single HDD with 7,200 rpm provides 75-150 IOPS, and a single HDD with 15,000 rpm provides 175-210 IOPS. The specific value depends on factors such as access mode (sequential or random) and I/O size.



### Snapshot chain

A snapshot chain is the relationship chain made up of all the snapshots of the same disk. Each node represents one snapshot of the disk.



### MBR

See [MBR](https://intl.cloud.tencent.com/document/product/362/18555)



### GPT

GUID Partition Table (GPT) is the partition format of a physical disk. It is a part of the Extensible Firmware Interface (EFI) standard and is a replacement for the MBR partition table used by most existing disks.

### Full snapshot

A full snapshot is the first snapshot created for a disk that saves all data on the disk.



### Sequential I/O

Sequential I/O means that read-write operations sequentially access data of a logic block from adjacent addresses. The sequential I/O access greatly reduces the disk seek time because the read-write disk head barely needs to move to access the next block. Services such as data backups and log writing usually generate sequential I/O.

### Random I/O

Random I/O means that the access addresses are not sequential, but randomly distributed in the address space of the LUN disk. Services that primarily generate random I/O include OLTP service, SQL, and instant messaging services.



### Striping

Striping is an automatic technique to balance I/O loads across multiple physical disks.

### Throughput

The throughput is the volume of data successfully transmitted in a given unit of time over a network, device, port, virtual circuit or other devices.



### Cloud disk snapshots

A cloud disk snapshot is used to save a copy of the cloud disk at a point in time. You can use the snapshot to restore the cloud disk to the point in time when the snapshot was created.



### Incremental snapshot

An incremental snapshot is the subsequent snapshot that only backs up files added or modified after a full snapshot or the previous incremental snapshot.

### MBR

Master Boot Record (MBR) is the sector that must be read first when a computer accesses the disk after being started. The MBR records information about the hard disk itself, and the size as well as location of all partitions on the disk. It is also an important entry for data information.