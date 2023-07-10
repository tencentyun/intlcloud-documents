

### Elastic cloud disks

An elastic cloud disk has an independent lifecycle (billing cycle) and can be mounted and unmounted between different CVM instances in the same region and availability zone. However, it cannot be mounted simultaneously on multiple CVMs.



### Non-elastic cloud disks

A non-elastic cloud disk is created along with a Cloud Virtual Machine (CVM) and has the same lifecycle as the CVM. It does not support elastic mounting.



### GPT

Please see [GPT](https://www.tencentcloud.com/document/product/362/18555#gpt2).



### Rollback

A rollback restores a program or data to the last correct status when a processing error occurs. The two types are program rollback and data rollback.



### IOPS

Input/Output Per Second (IOPS) refers to the number of reads (outputs) and writes (inputs) in one second. It is an important metric to measure the disk performance. IOPS indicates the number of I/O requests the system can process in a unit of time (per second). I/O requests are generally data read or write requests.
Traditional disks are essentially mechanical devices, such as FC, SAS and SATA disks, whose spin rates are usually 5,400/7,200/10,000/15,000 rpm. The key factor affecting a disk is the disk service time, that is, the time it takes for the disk to complete an I/O request. This consists of seek time, rotational delay, and data transfer time.
In general, a single HDD with 7,200 rpm provides 75-150 IOPS, and a single HDD with 15,000 rpm provides 175-210 IOPS. The actual value depends on factors such as access mode (sequential or random) and I/O size.



### Snapshot chain

The snapshot chain is a relationship chain composed of all snapshots of the same disk, and each node represents one snapshot of the disk.



### MBR

See [MBR](https://www.tencentcloud.com/document/product/362/18555#mbr2)



### GPT

GUID Partition Table (GPT) is the partition layout of a physical disk. It is a part of the Extensible Firmware Interface (EFI) standard and a replacement for the MBR partition table used by most disks.

### Full snapshot

A full snapshot is the first snapshot created for a disk that saves all data on the disk.



### Sequential I/O

Sequential I/O means logical blocks are read and written sequentially from adjacent addressees. In sequential I/O access, the seek time of a disk is greatly reduced because the read-write heads barely need to move when accessing the next block. Services such as data backup and logging are sequential I/O.

### Random I/O

Random I/O means access addresses are not sequential, but randomly scattered on various parts of the disk. Services such as OLTP, SQL, and instant messaging are random I/O.



### Striping

Striping is a method to automatically balance I/O loads across multiple physical disks.

### Throughput

Throughput is the amount of data successfully transferred in a given unit of time over a network, device, port, virtual circuit or other devices.



### Cloud disk snapshots

A snapshot is used to save a copy of the cloud disk at a point in time. You can use it to restore the cloud disk to the point in time when the snapshot was created.



### Incremental snapshot

An incremental snapshot is a point-in-time backup that consists only of all the changes since the full snapshot or the previous incremental snapshot.

### MBR

Master Boot Record (MBR) is the first sector that the computer must read when accessing the disk after startup. MBR records information about the disk, and the size and location of each partition of the disk. It is also an important entry for data information.
