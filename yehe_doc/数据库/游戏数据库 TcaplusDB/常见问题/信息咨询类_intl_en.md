- [Does TcaplusDB support data removal?](#41)
- [What are the data structures of TcaplusDB?](#43)
- [What is the single-instance memory capacity and CPU utilization of the TcaplusDB SDK?](#67)
- [How many tables are in a table group in TcaplusDB?](#68)
- [What are the restrictions on the key and value fields in TcaplusDB?](#69)
- [How long is the TcaplusDB backup file retained?](#72)
- [Is the game server connected to all tcaproxy (access layer)?](#73)
- [How do I perform data analysis of TcaplusDB data?](#74)
- [What is the maximum size of a single table in TcaplusDB? What is the limit on the number of records?](#82)
- [Does TcaplusDB support multi-table transaction operations and batch write operations?](#85)
- [Is the TcaplusDB API upgrade backward compatible?](#88)

<span id="41"></span>
### Does TcaplusDB support data removal?
TcaplusDB supports table-level data removal, where the data is removed according to the last time it is written. 
<span id="43"></span>
### What are the data structures of TcaplusDB?
TcaplusDB supports data structures such as list array, queries by part of keys (indexes), key-value, key-object (that is, the value of a single key can be arbitrary data structures, for example, game server can serialize `lua table` into the value field).

<span id="67"></span>
### What is the single-instance memory capacity and CPU utilization of the TcaplusDB SDK?
The maximum single-instance memory consumption is 73 MB, and the maximum CPU utilization is 30%.

<span id="68"></span>
### How many tables are in a table group in TcaplusDB?
In TcaplusDB, a table group can have up to 256 tables. If there are more than 256 tables in a table group, you can add a new table group or merge the tables. If you need technical support, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) and select **Others** on the **Select your products** page.

<span id="69"></span>
### What are the restrictions on the key and value fields in TcaplusDB?
The number of key fields of the generic table is 4, the number of key fields of the list table is 3, and the size of a single key field is 1,024 B. The number of value fields of the generic table is 128, the number of value fields of the list table is 127, the size of a single value field is 256 KB, and the maximum size of a record is 1 MB.

<span id="72"></span>
### How long is the TcaplusDB backup file retained?
The engine files backed up by TcaplusDB are retained for 7 days, and the Ulog is saved for 7 days. The retention periods vary with TcaplusDB environment. For the retention period of a specific TcaplusDB environment, you can [contact customer service](https://intl.cloud.tencent.com/support).

<span id="73"></span>
### Is the game server connected to all tcaproxy (access layer)?
In order to reduce the cost of maintaining the TCP connections between the game server and tcaproxy (access layer), the game server supports selecting some tcaproxy (access layer) to establish connections.

<span id="74"></span>
### How do I perform data analysis of TcaplusDB data?
TcaplusDB data can be exported in any format, including json, pb and other formats, and can be imported into data analysis systems such as TDW. TcaplusDB supports the import of real-time data into MySQL databases and so on.

<span id="82"></span>
### What is the maximum size of a single table in TcaplusDB? What is the limit on the number of records?
A single table can be subdivided into 10,000 data shards, each data shard is 256 GB, that is, the total size of a single table is 10,000 * 256 GB. A single table has no limit on the number of records, and the number of records in a single table is related to the size of a single record.

<span id="85"></span>
### Does TcaplusDB support multi-table transaction operations and batch write operations?
TcaplusDB supports neither multi-table transaction operations nor batch write operations. To perform multi-table transaction operations, changes have to be made at your business side. In TcaplusDB, operations have to be done in sequence. For example, when multiple operations are submitted at the same time, all completed operations are rolled back if one of the subsequent operation fails. After the rollback, you can submit these operations again. For important operations, we recommend keeping the logs.

<span id="88"></span>
### Is the TcaplusDB API upgrade backward compatible?
TcaplusDB API upgrade is backward compatible, and existing APIs, command words, and features will not be modified.
