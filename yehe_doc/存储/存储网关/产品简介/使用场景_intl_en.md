### Storage Resource Allocation
Expanding the capacity of local NAS and SAN storage arrays not only results in high device and labor costs but also poses a challenge to storage architecture design. After CSG is deployed to connect cloud storage with local storage system architecture, the hybrid cloud storage workload can be automatically coordinated when data migration or big data analytics are needed or business data volume surges.

### Hot/Cold Data Separation
Storing all business data on local devices not only leads to high costs but also increases the burden of OPS.
The hot cache feature of CSG can automatically cache hot data locally that requires high access performance and upload delay-insensitive colder data to the cloud storage, which achieves hot/cold data separation. Meanwhile, when the proportion of cold and hot data changes, the proportion of local cache and cloud storage can be scaled as needed to reduce the costs of use.

### Backup and Archiving
After the data is uploaded to the cloud storage, the data will be stored according to multiple backup policies to maintain data persistence. In addition, each data version can be backed up and archived by creating a scheduled snapshot.

### Disaster Recovery
Snapshots can be taken of the volumes and stored in COS and they can be used to restore the volumes mounted to CSG. When an active system encounters an accident, the data can be easily restored from the snapshots for business continuity by reconfiguring CSG on the CVM instance or in another IDC.

### Data Processing and Distribution
Files uploaded to COS through file gateway can be used for other Tencent Cloud products such as CDN, Cloud Infinite, Media Processing Service to provide a "storage + processing" solution.

