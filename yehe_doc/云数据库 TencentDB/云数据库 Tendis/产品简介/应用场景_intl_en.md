### Ecommerce
Ecommerce applications generally have massive amounts of item data. Using TencentDB for Tendis Hybrid Storage Edition can easily break through the memory capacity limit and greatly reduce business costs. In normal business requests, data of active items will be read from the memory, while data of inactive items will be read from the disk, which can eliminate the trouble of insufficient memory.

### Live Streaming
Data of live streaming businesses often can be obviously divided into hot data and cold data, where access requests to trending live rooms account for the vast majority. TencentDB for Tendis Hybrid Storage Edition retains data of such rooms in the memory, and stores data of inactive rooms on the disk. This can achieve a better balance between user experience and business costs.

### Gaming
Gaming businesses usually generate massive amounts of player data. By using TencentDB for Tendis Hybrid Storage Edition, data of online active players will be continuously cached in the memory, while data of inactive players will be evicted from the memory and automatically cached when they become active again. This greatly reduces the storage costs. Operating staff only need to access Tendis without concerns over the logic of cache and storage swap in the business, which significantly improves the efficiency of version iteration.
