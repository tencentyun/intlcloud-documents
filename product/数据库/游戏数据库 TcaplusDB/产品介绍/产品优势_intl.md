### Low cost
The key-table NoSQL storage service, which employs memory storage supplemented by disk storage, provides the ability of switching in-process data between memory and disks, and the ability of dynamically expanding capacity across multiple processes to ensure that active data are stored in memory and inactive data on disks. This service saves about 70% in costs compared to memory-only storage, and about 40% in comparison to Redis+MySQL.

### High performance
Features including exchange of hot and cold data between memory and disks based on the Least Recently Used (LRU) algorithm, data storage on SSD disk and multi-server distribution of data ensure a high performance of up to 100,000 QPS per server with a latency less than 10 milliseconds.

### High availability
The master/slave hot backup mechanism ensures quick recovery in case of system failure.

### Support for game-specific needs
Game-specific needs such as a multi-server/multi-region model, quick start-up of servers, cross-region access, cross-region data consolidation, data compression and more are met, and are optimized continuously according to game requirements.

### Dynamic expansion
The storage space is uncapped, and the capacity can be dynamically expanded or reduced according to the actual needs of a game without affecting game operation. This feature makes it easier to address sudden changes in business scale.

### Ease of learning
The service inherits the development technologies of the PC platform and benefits from the development experience of the PC game team. The service API provides easy synchronous and asynchronous operation APIs.

### Service-based operation
With a convenient resource application mode, there will no longer be any need to manually deploy the storage service environment.

### Optimization of resource utilization to improve operational efficiency
Alarm and other basic systems are integrated to provide process-level monitoring capabilities. Service APIs provide easy access to server capacity expansion, load balancing, and disaster recovery.
