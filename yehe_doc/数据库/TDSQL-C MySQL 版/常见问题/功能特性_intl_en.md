### How long does it take to adjust the database configuration? Will this affect my business?
TDSQL-C for MySQL configuration adjustment includes computing specification adjustment and storage space adjustment.
- Computing specification adjustment
 - In a non-serverless billing mode, computing specification adjustment can be completed in seconds, but there may be a momentary disconnection of 3–5 seconds. Make sure that your business has an automatic reconnection mechanism. We recommend you perform this operation during off-peak hours.
 - In serverless billing mode, the upper and lower limits of the computing power are adjusted automatically, and no momentary disconnections will occur to affect the business.
- Storage space adjustment
In pay-as-you-go billing mode, you don't need to manually adjust the storage space size, and the system will bill you hourly by actual usage. In monthly subscription billing mode, the prepaid storage space to be changed to must be greater than the used storage space. Changing the billing mode of the storage space won't affect the business.

### How long does it take to add a read-only instance? Will this affect my business?
It takes less than 30 seconds to add a read-only instance, which has no impact on your business. The time it takes has nothing to do with the instance storage space. For detailed directions, see [Creating Read-Only Instance](https://intl.cloud.tencent.com/document/product/1098/40631).

### Is there a replication delay between a read-write instance and a read-only instance?
Traditional cloud databases have a delay of seconds, but TDSQL-C for MySQL uses redo logs for replication, which greatly reduces the delay to milliseconds.

### In which cases will the replication delay increase?
The replication delay in TDSQL-C for MySQL is much shorter than that in traditional databases, and you can view the **Redo Log Based Replication Lag of Replica Instance** metric of the instance to check the actual delay.
The replication delay will increase in the following cases:
- The write load of the read-write instance is too high, and too many redo logs are generated, which cannot be applied by the read-only instance in time.
- The load of the read-only instance is too high, which preempts too many resources that should be used for redo logs.
- The I/O bottleneck is hit, severely slowing down redo log reads/writes.

### How do I perform automatic failover?
TDSQL-C for MySQL adopts a high-availability cluster architecture. The system automatically detects failed nodes and starts a new compute node to replace the failed one and continue providing read-write access.

### Can the RPO be guaranteed at zero when a single node fails?
Yes. TDSQL-C for MySQL uses the smart storage tiering mechanism based on three replicas to guarantee the data integrity after failover, where hot data is stored in fast storage (NVMe + SSD replica), warm data is stored in low-redundancy storage (SSD EC), and cold data is stored in slow storage (HHD).

### How do I add fields and indexes online?
TDSQL-C for MySQL supports native MySQL online DDL and open-source tools pt-osc and gh-ost. In addition, it also supports instance DDL operations for special scenarios. For more information, see [Instant DDL Overview](https://intl.cloud.tencent.com/document/product/1098/44589).

### Is BULK INSERT supported when there is only data write? How many values at most can be inserted at a time?
Yes. The maximum number of values that can be inserted at a time is determined by the `max_allowed_packet` parameter. You can modify it in the console to specify the limit. The value must be a multiple of 1,024 between 1,024 and 1,073,741,824. For detailed directions, see [Setting Instance Parameters](https://intl.cloud.tencent.com/document/product/1098/44602).
