<div class="tab_list">
<ul>
    <li><a href="#A-E">A-E</a></li>
    <li><a href="#F-J">F-J</a></li>
    <li><a href="#K-O">K-O</a></li>
    <li><a href="#P-T">P-T</a></li>
    <li><a href="#U-Z">U-Z</a></li>
</ul>
</div>  

<span id="A-E"></span>
## A-E 
### Tape  
This is a storage space that can be mounted to a tape gateway. A tape gateway can mount up to 7,200 tapes of up to 4 TB storage capacity each.

<span id="F-J"></span>
## F-J 
### High-IO gateway  
In addition to the universal type, file gateway also provides a high-IO type. High-IO gateways are suitable for application scenarios with high egress bandwidth or Direct Connect lines. They can upload data to the public cloud more quickly. If you have a high amount of data that needs to be migrated to the public cloud for backup or archiving, you can select a high-IO gateway. Note: the minimum server memory configuration for a high-IO gateway is 64 GB.  
### High-speed mode  
Universal gateway provides both "stable" and "high-speed" operation modes. In high-speed mode, data is first written to the memory and then written to the disk from the memory, and the write result is returned right after writing. It is suitable for scenarios with high response speed requirements. However, a success is returned as soon as the data is written to the memory in this mode, and if exceptions such as unexpected power failure happen before the data is written to the disk, the data cached in the memory may be lost. For more information on stable mode, please see <a href="#jump" target="_self">Stable mode</a>.  
### Archive  
When using a tape gateway, you can transfer tapes that do not need to read data frequently from COS to CAS for storage, and this process is called tape archiving. After the data is stored in CAS, the storage is charged as an archived tape, further reducing the storage costs of the backup data.  
### Volume  
This is a storage space that can be mounted to a volume gateway. A gateway can mount up to 4,096 volumes of up to 1 PB storage capacity each.  
### Cache  
This is a storage space used to store frequently accessed hot data in local storage (local disks, DAS, SAN).

<span id="K-O"></span>
## K-O 
### Snapshot  
Snapshot is a data backup method provided by Tencent Cloud. It can create a fully available copy of the specified source volume whose lifecycle is independent of the source volume. The snapshot includes an image of the volume at the point in time when copy is started.

<span id="P-T"></span>
## P-T 
### Retrieval  
If you need to read the data in an already archived tape, you need to retrieve the archived tape from CAS back to COS, and the retrieved tape is read-only (not writable).
### Upload buffer  
This is a storage space used to temporarily store the content to be uploaded in local storage (local disks, DAS, SAN).
### Universal gateway
It is suitable for most application scenarios and does not require high egress bandwidth.

<span id="U-Z"></span>
## U-Z
### Gateway  
This is an agent executed locally by the user and converts COS or CAS to a local iSCSI, NAS or VTL storage device based on the selected gateway type.  
### File system  
This is a storage space that can be mounted to a file gateway. A file gateway can mount up to 4,096 file systems of up to 1 PB storage capacity each.  
### <span id = "jump">Stable mode</span>  
Universal gateway provides both "stable" and "high-speed" operation modes. In stable mode, data is written directly to the disk. The write result will be returned only after the data falls into the disk. The stability of data written in this mode is high, and data can be restored in the event of exceptions such as unexpected power failure.  
### Metadata disk  
This stores the metadata of the files stored in the file system in local storage (local disks, DAS, SAN). It is required to be configured for file gateway.

