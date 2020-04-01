
### Does the data subscription feature allow multiple SDKs to connect to and consume the same channel simultaneously?
No. A channel can only be connected to and used by one SDK for consumption at a time. If you have multiple downstream SDKs to subscribe to the same table, please create multiple channels.

### Does the data subscription feature allow one SDK to connect to multiple channels?
Yes. An SDK can consume multiple channels at a time.

### Why does the error "already has sdk on this channel" occur when an SDK is started?
A channel can only be connected to by one SDK for consumption. If another connection is created, this error will occur. In this case, you need to check whether the application has exited. If the error persists, you can set the restart interval a little longer, such as 20 seconds.

### Does the real-time incremental data in data subscription refer to the added data only or include the modified data?
The incremental data that can be subscribed to through data subscription includes all INSERT/DELETE/UPDATE changes (DML) and structure changes (DDL).

### A TencentDB instance and a local database have the same table structure but different indices. Can they be synced in real time by using the data subscription feature?
Yes. Data subscription only covers data changes, and it does not matter if the indices are different. However, if you have subscribed to structure changes and your TencentDB instance involves index changes, local consumption of structure changes may fail if the indices are different.

### Why can't I modify the consumption time point of a data subscription channel?
When this error occurs, relevant prompts will be displayed on the screen. Generally, it is because that the downstream SDK connected to the subscription channel is still consuming data. You can go to the DTS Console to view the consumption source IP and check whether the downstream SDK is consuming data, and if yes, you need to stop the consumption first before you can modify the consumption time point.

### How can I determine whether data consumption is normal?
When data is written to a channel (or not all data is consumed), the consumption time point in the console can be migrated normally if data consumption is normal.

### If a data entry on the consumer side is not acknowledged for data subscription, why does the SDK receive duplicate data entries after restart?
If there is any unacknowledged message, the SDK will keep pulling it until the SDK cache is full. At this time, the consumption time point saved on the server will be the time point of the last message before it is acknowledged.
When the SDK is restarted, the server will push data again from the consumption time point of the unacknowledged message to avoid message loss. Therefore, the SDK will receive some repeated messages.

### Why can't data be successfully subscribed to if the SDK is restarted days after exit? The error message reads "Maybe checkpint is too old".
The data in the data subscription channel will be retained for 1 day and then deleted. If the time point of the last consumed data entry before the SDK exits is -1 day ago, then the data at the consumption time point cannot be subscribed to successfully. To fix this problem, you need to modify the consumption time point to ensure it is within the valid range.

### When pulling data, the SDK suddenly crashed and couldn't subscribe to any data; after restart, it consumed some data before crashing again. Why?
This is probably because the ackAsConsumed API is not called to report the consumption time point in the SDK code. In this case, the data in the limited cache space of the SDK will not be deleted. When the cache is full, new data cannot be pulled, so the SDK will crash and fail to subscribe to any data.
>All messages here, including BEGIN and COMMIT messages and those irrelevant to the business logic, must be acknowledged for consumption.

### How do I ensure that the data subscribed to by the SDK is a complete transaction? Will the record in the middle of the transaction be pulled based on the specified consumption time point?
No. Based on the user-specified consumption time point or the time point of the last acknowledged consumption, the server will search for the start point of the complete transaction corresponding to this consumption time point. Data is sent to the downstream SDK from the beginning of the transaction. Therefore, the full data of the complete transaction can be received.

### Will any problem in data subscription occur upon TencentDB master/slave switchover or master restart? Will data be lost?
No. In case of master/slave switchover or master restart, data subscription will automatically perform switch imperceptibly to the SDK.

### Why does the error "Do DTS authentication fail, caused by: get channel info from msg failed" occur when the SDK is started?
You need to verify whether the input parameters are correct, including `ip`, `port`, `secretId`, `secretKey`, and `channelId`.

### Why does the system prompt that `secretId` has no permission when the SDK is started?
A sub-account has no permission by default. It must be granted access to the `name/dts:AuthenticateSubscribeSDK` operation or all DTS operations through the `QcloudDTSFullAccess` policy by the root account.
>You need to create the `QcloudDTSFullAccess` policy on your own as it is not predefined in CAM.

- Grant the SDK access permission to all channels:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "dts:AuthenticateSubscribeSDK"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
- Grant the SDK access permission to a specified channel:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "dts:AuthenticateSubscribeSDK"
            ],
            "resource": "qcs::dts:::channel/{channelId}",
            "effect": "allow"
        }
    ]
}
```


### Will duplicate date be received through data subscription?
No, if data consumption is normal. However, there is a very slim chance that if the SDK quits abnormally and the last acknowledged consumption time point is not reported promptly, duplicate data may be received when the SDK is started next time.
If a complete transaction is not acknowledged, the data will be pulled again from the beginning of the transaction when the SDK is started again. In this case, the data cannot be regarded as duplicate data. The core logic of the SDK will ensure the transaction integrity. 

### Can a data subscription instance subscribe to multiple TencentDB instances?
No. A data subscription instance can only subscribe to one TencentDB instance.

### What should I do if OOM occurs while the SDK is running?
You are recommended to use a host with higher specification. When a single SDK runs smoothly at a high speed, it consumes less than 1 core of CPU and less than 1.5 GB of memory.
