[//]: # (chinagitpath:XXXXX)

### Low cost
The key-table NoSQL storage service, which employs memory storage supplemented by disk storage, provides the ability of switching in-process data between memory and disks, and the ability of dynamically expanding capacity across multiple processes to ensure that active data are stored in memory and inactive data on disks. This service saves about 70% in costs than the memory-only storage and about 40% than Redis+MySQL.

### High performance
Features including LRU-based exchange of hot and cold data between memory and disks, data storage on SSD disk and multi-server distribution of data ensure a high performance of up to 100,000 QPS per server with a latency less than 10 milliseconds.

### High availability
The master/slave hot backup mechanism ensures quick recovery in case of system failure.

### Support for game-specific needs
The multi-server/multi-region model, quick start-up of servers, cross-region access, cross-region data consolidation, data compression and other game-specific abilities are provided and are optimized continuously according to game needs.

### Dynamic expansion
The storage space is uncapped, and the capacity can be dynamically expanded or reduced according to the actual needs of a game without affecting the running of the game. This feature makes it easier to address sudden changes in business scale.

### Ease of learning
The PC game team can learn from our PC game development technologies. Service APIs contain simple synchronous and asynchronous operation APIs.

### Service-based operation
With convenient resource application method, you don't need to deploy the storage service environment for your business manually.

### Optimization of resource utilization to improve operational efficiency
Alarm and other basic systems are integrated to provide process-level monitoring capabilities. Service APIs provide easy access to server capacity expansion, load balancer, and disaster recovery.

