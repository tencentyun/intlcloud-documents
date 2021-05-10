### Alias

An alias is used to abstract the name of a fleet. By using an alias instead of a specific fleet ID, you can change the server fleet associated with the alias to switch player traffic from one fleet to another fleet more easily and seamlessly for zero downtime updates.



### Queue

- In GSE, a queue is a group of server fleets running in regions of a game asset package. You can use a queue to create a cross-region fleet group and allows placing game server sessions in any fleet in the queue, so as to minimize the delay, deliver a better player experience, use more fleet capacity more efficiently, provide high capacity for new games more swiftly, and make the game more elastically available.
- In Cloud Message Queue (CMQ), a queue is the destination of message storage, from which consumers actively get messages. In a queue, `MessageId ` or `ReceiptHandle` is used to uniquely identify messages.



### Server Fleet

A server fleet is a group of managed resources in the form of Cloud Virtual Machine (CVM) instances capable of auto scaling and health check. The managed server fleet is used to deploy game servers.



### Asset Package

An asset package is a zip package deployed on a CVM instance. Its directory must contain all the components necessary for running your game server, including executable files, dependent packages, and installation scripts of the game server.

### Instance

- In GSE, an instance is a CVM instance to host a game server on. For instance types, see [Game Server Elastic-scaling](https://console.cloud.tencent.com/gse/asset) console.
- In TI-ONE, an instance is created each time a workflow runs. Instance types include historical instances, parameter instances, re-run instances, and timed instances.
- In Tencent Kubernetes Engine (TKE), an instance consists of one or more associated containers that share the same storage and network space.
- In BatchCompute, an instance is a CVM instance, the smallest unit that this service can schedule. You can specify one or more instances for each job.
- In Data Security Governance Center (DSGC), an instance generally represents the unit of data asset in Tencent Cloud, and varies by service. For example, it is a database for TencentDB, and a bucket for COS.
- In Tencent Container Registry (TCR), an instance is purchased in a selected region to provide a dedicated container image hosting service. You do not need to share your instance with other users for backend service and storage of your core data. In Docker, a TCR instance is like an independent Docker Registry instance, that is, you purchase and deploy a private Docker Registry instance in the cloud.
