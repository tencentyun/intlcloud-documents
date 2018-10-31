## Gateway
This is an agent executed locally by the user and converts COS or CAS to a local iSCSI, NAS or VTL storage device based on the selected gateway type.

## Volume
This is a block storage space provided by a volume gateway. A gateway can mount up to 4,096 volumes, and a volume has a maximum capacity of 1 PB.

## File System
A COS bucket can be used as a file system, and a file gateway can support up to 4,096 file systems.

## Tape
This is a storage space that can be mounted to a tape gateway. A tape gateway can mount up to 7,200 tapes, and a tape has a maximum capacity of 4 TB.

## Snapshot
This is a data backup method provided by Tencent Cloud. By creating a fully available copy of the specified volume, it makes the backup independent of the lifecycle of the volume. The snapshot includes an image of the volume at the point in time when copying is started. Tencent Cloud stores the user-created snapshots in a distributed and redundant manner in COS, further ensuring the backup reliability. Snapshots are incremental backups. This means only the changed data in the device after the most recent snapshot is created will be stored, which minimizes the time it takes to create a snapshot and reduces storage cost. Snapshots are billed as part of the final storage usage.
You can create a new volume based on a snapshot, so that the newly created volume in its initial state has the data in the snapshot as an exact copy of the original volume. Snapshots can be used to recover volumes across regions, but as cross-region data replication is required, recovering volumes from off-site snapshots incurs cross-region replication fees.

## CSG Disk
A disk can be configured for CSG to cache the written data, frequently read data and file metadata.

### Cache Disk
This is a storage space used to store frequently accessed hot data in local storage (local disks, DAS, SAN). It is required to be configured for volume and tape gateways.

### Upload Buffer Disk
This is a storage space used to temporarily store the content to be uploaded in local storage (local disks, DAS, SAN). It is required to be configured for volume, tape and file gateways.


### Metadata Disk
This stores the metadata of the files stored in the file system in local storage (local disks, DAS, SAN). It is required to be configured for file gateway.


## Stable/high-speed Mode
Volume gateway provides both "stable" and "high-speed" modes of operation. The two modes have the following differences and can be flexibly selected according to business needs.

- High-speed mode: Data is first written to the memory and then written to the disk from the memory, and the write result is returned right after writing. It is suitable for scenarios with high response speed requirements. However, a success is returned as soon as the data is written to the memory in this mode, and if exceptions such as unexpected power failure happen before the data is written to the disk, the data cached in the memory may be lost.
- Stable mode: Data is written directly to the disk. The write result will be returned only after the data falls into the disk. The stability of data written in this mode is high, and data can be restored in the event of exceptions such as unexpected power failure.

## Archiving
When using a tape gateway, you can transfer tapes that do not need to read data frequently from COS to CAS for storage, and this process is called tape archiving. After the data is stored in CAS, the storage is charged as an archive tape, further reducing the storage cost of the backup data.

## Retrieving
If you need to read the data in an already archived tape, you need to retrieve the archived tape from CAS back to COS, and the retrieved tape is read-only (not writable).





