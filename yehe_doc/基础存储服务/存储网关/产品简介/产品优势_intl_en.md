### Out-of-the-Box Functionality

Cloud storage uses HTTP Restful APIs, while enterprise applications or storage systems typically use traditional protocols and thus do not have direct access to cloud storage services. With the aid of CSG, you only need to download a ready-to-use CVM instance that contains the gateway to mount public cloud storage as local iSCSI or NFS storage, with no secondary development or addition of rack slots, power supply or cooling devices required.

### Massive Storage Capacity

CSG provides massive storage capacity. A single volume or file system can be up to 1 PB, and a single gateway can hold up to 4,096 volumes with the "resize" feature supported. In addition, CSG uses a caching mechanism to separate hot and cold data by caching frequently read hot data locally and asynchronously uploading colder data to the cloud according to the network configuration. In this way, users or programs can enjoy the performance of local disk and network, balance the access latency and gain the capability of unlimited cloud storage.

### High Cost-Effectiveness and Efficiency

You don't have to pay for hardware devices and daily OPS. Cloud storage is pay-per-use with no minimum usage limit and can be expanded unlimitedly. Volume snapshots save only the incremental portion at a time, reducing the storage capacity required.

### Security and Persistence

The data is locally parted, compressed and encrypted before uploaded to the cloud, maintaining data security and integrity. The cloud storage provided by COS and CAS uses a three-copy storage mechanism and erasure coding technology to provide 99.999999999% data persistence and protect the stability and security of all data.


