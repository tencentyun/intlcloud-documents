## What Is CSG?
Cloud Storage Gateway (CSG) is a hybrid cloud storage solution designed to help organizations and individuals seamlessly connect local storage to a public cloud. It eliminates your concerns over compatibility of multi-protocol local storage devices with cloud storage. Once installed locally, it enables you to achieve a hybrid cloud deployment with massive cloud storage capacity and high performance comparable to local storage.

## Types of Gateways
### Volume Gateway
After deploying a volume gateway in local network or public cloud environments, COS can be mounted as an Internet Small Computer System Interface (iSCSI) device to the local application server. Volume gateway not only maintains low latency for hot data access, but also significantly reduces primary data storage costs while minimizing the need for local storage expansion.

### File Gateway
After deploying a file gateway in local network or public cloud environments, COS can be mounted as a Network File System (NFS) for multiple servers. File gateway eliminates the need for file system installation from scratch. The POSIX file protocol can be used for reads and writes of objects on COS. Files uploaded to COS through the gateway can be utilized for artificial intelligence and big data services such as CDN, voice recognition, OCR and Mapreduce.

There are also file gateways that support CIFS/SMB protocols where data reads and writes can only be done through CSG. If needed, you can apply for a trial by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).

### Tape Gateway
After deploying a tape gateway in local network or public cloud environments, CAS (Cloud Archive Storage) can be used as a more cost-effective and durable storage for backing up and archiving data. Tape gateway provides a virtual tape library (VTL) that scales seamlessly in your local network environment based on your business needs, eliminating the costs of pre-configuration, expansion and OPS for physical tape libraries.


## Features
### Protocol Conversion
CSG supports directly mounting public storage with RESTful APIs to local networks as iSCSI, NFS/SMB/CIFS or VTL for immediate use. Organizations that have already deployed infrastructure can access the public cloud through CSG for higher cloud storage capacity, lower costs and greater flexibility while no longer requiring changes to the existing network structure or development of APIs for network program alignment.

### Accelerated Access
CSG uses cache optimization algorithms to store frequently accessed hot data locally and transfer colder data to the cloud storage. This enables faster obtaining of frequently used data compared to directly connecting to the public cloud. Further, with the aid of elastic cloud storage, only the storage capacity required by fast access cache needs to be provided, which more effectively reduces infrastructure and OPS costs.

### Snapshot and Data Recovery
Snapshots can be created on a regular basis to back up changing data in volume storage to the cloud-based IDC. If the local storage fails or historical data needs to be restored to a previous point in time, the volumes mounted to CSG or CVM can be restored from a snapshot at any time.

### Network Resource Adjustment
CSG compresses local data before uploading it to the cloud to optimize the transfer efficiency and supports configuring uplink/downlink transfer speed limits to help make full of egress bandwidth resources and reduce data transfer costs.


