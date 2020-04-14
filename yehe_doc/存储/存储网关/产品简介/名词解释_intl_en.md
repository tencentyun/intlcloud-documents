### Gateway
This is an agent executed locally by the user and converts COS or CAS to a local iSCSI, NAS or VTL storage device based on the selected gateway type.

### Volume
This is a block storage space provided by a volume gateway. A gateway can mount up to 4,096 volumes of up to 1 PB storage capacity each.

### File System
A COS bucket can be used as a file system, and a file gateway can support up to 4,096 file systems.

### Tape
This is a storage space that can be mounted to a tape gateway. A tape gateway can mount up to 7,200 tapes of up to 4 TB storage capacity each.

### Snapshot
Snapshot is a data backup method provided by Tencent Cloud. It can create a fully available copy of the specified volume whose lifecycle is independent of the source volume. The snapshot contains the image of volume at the point in time when the copy starts. Tencent Cloud stores the user-created snapshots in a distributed and redundant manner in COS, further ensuring the backup reliability. Snapshots are incremental backups. This means only the changed data in the device after the most recent snapshot is created will be stored, which minimizes the time it takes to create a snapshot and reduces storage costs. Snapshots are billed as part of the final storage usage.
You can create a new volume based on a snapshot, so that the newly created volume in its initial state has the data in the snapshot as an exact copy of the original volume. Snapshots can be used to recover volumes across regions, but as cross-region data replication is required, recovering volumes from off-site snapshots will incur cross-region replication fees.

### CSG disk
A disk can be configured for CSG to cache the written data, frequently read data, and file metadata.

#### Cache
This is a storage space used to store frequently accessed hot data in local storage (local disks, DAS, SAN). It is required to be configured for volume and tape gateways.

#### Upload buffer disk
This is a storage space used to temporarily store the content to be uploaded in local storage (local disks, DAS, SAN). It is required to be configured for volume, tape and file gateways.


#### Metadata disk
This stores the metadata of the files stored in the file system in local storage (local disks, DAS, SAN). It is required to be configured for file gateway.


### Stable/High-Speed Mode
Volume gateway provides both "stable" and "high-speed" operation modes. The two modes have the following differences and can be flexibly selected according to business needs.

- High-speed mode: data is first written to the memory and then written to the disk from the memory, and the write result is returned right after writing. It is suitable for scenarios with high response speed requirements. However, a success is returned as soon as the data is written to the memory in this mode, and if exceptions such as unexpected power failure happen before the data is written to the disk, the data cached in the memory may be lost.
- Stable mode: data is written directly to the disk. The write result will be returned only after the data falls into the disk. The stability of data written in this mode is high, and data can be restored in the event of exceptions such as unexpected power failure.

### Archive
When using a tape gateway, you can transfer tapes that do not need to read data frequently from COS to CAS for storage, and this process is called tape archiving. After the data is stored in CAS, the storage is charged as an archived tape, further reducing the storage costs of the backup data.

### Retrieval
If you need to read the data in an already archived tape, you need to retrieve the archived tape from CAS back to COS, and the retrieved tape is read-only (not writable).





