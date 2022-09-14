## How migration works

- The [Siphon](https://github.com/imneov/ssdb-port) migration tool developed based on Go is disguised as the SSDB slave to subscribe to data and sync the data to Redis.
- Siphon is automatically connected to the SSDB server upon startup to perform key addressing. It starts sync from the starting position until all the existing data is synced and then syncs the incremental data. That is to say, the tool establishes a persistent connection after startup and keeps running.

## Tool and version descriptions

- Migration tool: [Siphon](https://github.com/imneov/ssdb-port). It applies to all SSDB kernel versions.
- If SSDB involves big keys or over 100 million keys, you need to [submit ticket](https://console.tencentcloud.com/workorder/category) to obtain the modified Siphon V2 version to improve data synchronization efficiency 

> ?The modified tool solves the problem of inefficiency of the native edition in data sync. In particular, it increases the efficiency in syncing big keys such as hashes and sorted sets (zsets) by about 12 times.

## Notes

Migration from SSDB in single-instance mode to Redis Cluster Edition involves logic compatibility issues, such as cross-slot transactions and pipelines.

## Migration directions

1. Collect the parameters required to run the migration command as shown below:
 - -p: Specifies the number of concurrent threads.
 - -f: Specifies the address of the SSDB server.
 - -t: Specifies the address of the Redis server.
 - -T: Specifies the password of the Redis database.
2. Start the migration tool with `siphon_v2 sync` and view the migration log.
```
./siphon_v2 sync -p 1 –f X.X.X.X:8888 -t X.X.X.x:6379 –T XXX
```
The status is displayed as follows after the command is executed:
 - **Copy Start**: Indicates the start of full data sync.
 - **Copy Stop**: Indicates the end of full data sync.
3. Wait for new data to be generated and incrementally synced to Redis without exiting the process.

