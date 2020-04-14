## What Is CSG?
Tencent Cloud Storage Gateway (CSG) is a hybrid cloud storage solution that helps organizations and individuals seamlessly connect local storage to a public cloud. It eliminates your concerns over compatibility of multiprotocol local storage devices with cloud storage. Once installed locally, it enables you to implement hybrid cloud deployment with massive cloud storage capacity that can be accessed as fast as with local storage.

## Types of Gateways
### Volume gateway
After a volume gateway is deployed in a local network or public cloud environment, COS can be mounted as an Internet Small Computer System Interface (iSCSI) device to the local application server. Volume gateway not only maintains low latency for hot data access, but also significantly reduces primary data storage costs while minimizing the need for local storage expansion.

### File gateway
After deploying a file gateway in local network or public cloud environments, COS can be mounted as a Network File System (NFS) for multiple servers. File gateway eliminates the need for file system installation from scratch. The POSIX file protocol can be used for reads and writes of objects on COS. Files uploaded to COS through the gateway can be utilized for artificial intelligence and big data services such as CDN, Automatic Speech Recognition, OCR, and Elastic MapReduce.

There are also file gateways that support CIFS/SMB protocols where data reads and writes can only be done through CSG. To try them out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

### Tape gateway
After deploying a tape gateway in local network or public cloud environments, CAS (archive storage) can be used as a more cost-effective and durable storage for backing up and archiving data. Tape gateway provides a virtual tape library (VTL) that scales seamlessly in your local network environment based on your business needs, eliminating the costs of pre-configuration, expansion, and OPS for physical tape libraries.


## Product Features
### Protocol conversion
CSG supports directly mounting public storage with RESTful APIs to local networks as iSCSI, NFS/SMB/CIFS or VTL for immediate use. Organizations that have already deployed infrastructures can access the public cloud through CSG for higher cloud storage capacity, lower costs, and greater flexibility with no changes to the existing network structure or development of APIs for network program alignment required.

### Accelerated access
CSG uses cache optimization algorithms to store frequently accessed hot data locally and transfer colder data to the cloud storage. Further, with the aid of elastic cloud storage, only the storage capacity required by fast access cache needs to be provided locally, which greatly reduces infrastructure and OPS costs.

### Snapshot and data recovery
Snapshots can be created regularly to back up the changing volume contents to cloud storage. If local storage fails or historical data needs to be restored, volumes mounted to CSG or CVM can be restored from snapshots to any points in time.

### Network resource adjustment
CSG compresses local data before uploading it to the cloud to optimize the transfer efficiency and supports configuring upstream/downstream transfer speed limits to help make full use of egress bandwidth resources and reduce data transfer costs.


