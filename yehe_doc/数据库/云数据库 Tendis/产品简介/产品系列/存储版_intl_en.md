TencentDB for Tendis Storage Edition (standard architecture) is based on Tendis, a KV (key-value) storage engine developed by Tencent. This Edition stores data on disks and supports multiple replicas to ensure service availability and data reliability, applicable to storing massive KV data.


## Features
#### Low cost
- The Storage Edition stores data on disks, ensuring data reliability at the storage level. It costs at least 80% less than the in-memory storage solution of Redis.
- The Storage Edition adopts the LZ4 data compression algorithm to automatically compress data once stored on disks. It can reach about 30% data compression ratio and achieve a better balance between performance and capacity.

#### High efficiency
The Storage Edition is compatible with most Redis commands and data structures, so the efficient Redis data structures and APIs can be used in your business.

#### Large capacity
Based on cloud disks, the Storage Edition provides a large storage capacity of 50 GB to 1.6 TB.

## Use Limits
TencentDB for Tendis Storage Edition is compatible with most Redis v4.0 commands. For more information, please see [Command Compatibility](https://intl.cloud.tencent.com/document/product/1083/39290). The unsupported data-related commands are listed in the following table.
>?If you need to use these unsupported commands, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

- **Unsupported commands**

| Command Group           | Command                | Compatibility |
|---------------|-------------------|-----|
| connection group  | swapdb            | x   |
| keys group        | randomkey         | x   |
| keys group        | touch             | x   |
| keys group        | object            | x   |
| keys group        | wait              | x   |
| keys group        | migrate           | x   |
| list group        | blpop             | x   |
| list group        | brpop             | x   |
| list group        | brpoplpush        | x   |
| sorted sets group | zpopmax           | x   |
| sorted sets group | zpopmin           | x   |
| sorted sets group | bzpopmax          | x   |
| sorted sets group | bzpopmin          | x   |
| scripting group   | eval              | x   |
| scripting group   | evalsha           | x   |
| scripting group   | script debug      | x   |
| scripting group   | script exists     | x   |
| scripting group   | script flush      | x   |
| scripting group   | script load       | x   |
| scripting group   | script kill       | x   |
| geo group         | geoadd            | x   |
| geo group         | geohash           | x   |
| geo group         | geopos            | x   |
| geo group         | geodist           | x   |
| geo group         | georadius         | x   |
| geo group         | georadiusbymember | x   |

- **Multi-database support**
TencentDB for Tendis Storage Edition supports the `SELECT 0` command but not multiple databases.

- **Poor-performance commands**
  - `linsert` and `lrem`: the `linsert` and `lrem` commands in the List command family have poor performance and are not recommended thus. They will traverse the list nodes in the disk with the O(n) execution time complexity. If there are many list nodes, the command execution will time out.
  - `append`: the `append` command performs poorly when the character size exceeds 1 MB.
