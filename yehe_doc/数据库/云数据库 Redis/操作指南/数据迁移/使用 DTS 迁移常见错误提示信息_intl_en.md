
## Issue 1
### Description
The following error message is displayed during migration with DTS:
```
[launch]state:6 #rdb rdbfile:./tmp1600869159_89068.rdb rdbsize:2753701723 rdb_writed_size:1606959104 rdb_parsed_size:0 rdb_parsed_begin:0 rdb_parsed_time:0 #replication master_replid:0549e2f0bdf373cef0c4c89bb0ce9e1757c4b105 repl_offset:1327777565448 write_command_count:0 finish_command_count:0 last_replack_time:0 #queue send_write_pos:0 send_read_pos:0 response_write_pos:0 response_read_pos:0 errtime:1600870264 errmsg:read rdb eof save rdb fail ready shutdown dts
```

### Cause
Check the log of the source Redis database. If it contains the following message, the `client-output-buffer-limit` configured for the source database is exceeded.
```
psync scheduled to be closed ASAP for overcoming of output buffer limits
```

### Solution
Run the following command to set the `client-output-buffer-limit` to infinite and initiate the DTS task again.
```
config set client-output-buffer-limit 'slave 0 0 0' 
```

## Issue 2
### Description
The following error message is displayed during migration with DTS:
```
[launch]state:8 #rdb rdbfile:./tmp1600395232_34851.rdb rdbsize:107994104 rdb_writed_size:107994104 rdb_parsed_size:107994104 rdb_parsed_begin:1600395238 rdb_parsed_time:5 #replication master_replid:995dba8ccffb7cc32a7c85de7b1632b952b74496 repl_offset:23851025 write_command_count:940765 finish_command_count:940763 last_replack_time:1600395298 #queue send_write_pos:440766 send_read_pos:440765 response_write_pos:440765 response_read_pos:440764 errtime:1600395297 errmsg:get rsp error:ERR value is not an integer or out of range command:*2 $4 INCR $35 APP_API_ORDER_CREATION_USER_4260882
```

### Cause
By capturing packets on two DTS Syncer instances in the region, it was found that the value of the key was characters rather than a number, causing the INCR execution to fail.
![](https://qcloudimg.tencent-cloud.cn/raw/17ee60d65cfe9f5bc0c812324fc201b6.jpg)
![](https://qcloudimg.tencent-cloud.cn/raw/543a24045e9825b82abaf2c7f3d601ac.jpg)

### Solution
Delete the relevant key and initiate the DTS migration again.

## Issue 3
### Description
The following error message is displayed during migration with DTS:
```
errmsg:Error reading bulk length while SYNCing:Operation now in progress read rdb length from src fail save rdb fail ready shutdown dts
```

### Cause
The error message of the source instance reveals that the RDB file does not have permission to access the directory.
![](https://qcloudimg.tencent-cloud.cn/raw/7135ab6a27b54ae470739fd08ea6eabf.jpg)

### Solution
Run the following command to set diskless replication and initiate the DTS task again.
```
config set repl-diskless-sync yes
```

## Issue 4
### Description
The following error message is displayed during migration with DTS:
```
[launch]state:6 #rdb rdbfile:./tmp1597977351_20216.rdb rdbsize:24282193511 rdb_writed_size:18683334200 rdb_parsed_size:0 rdb_parsed_begin:0 rdb_parsed_time:0 #replication master_replid:1b0da9f595cc40b795803eba3c9bea3aad1a1d68 repl_offset:921330115650 write_command_count:0 finish_command_count:0 last_replack_time:0 #queue send_write_pos:0 send_read_pos:0 response_write_pos:0 response_read_pos:0 errtime:1597978778 errmsg:write rdb data fail:456!=1696 error:No space left on device save rdb fail ready shutdown dts
```

### Cause
The disk space in the DTS Syncer instance is insufficient.

### Solution
Clear the disk in the DTS Syncer instance or mount a new disk and then initiate the DTS task again.

## Issue 5
### Description
The following error message is displayed during migration with DTS:
```
[launch]state:5 #rdb rdbfile: rdbsize:0 rdb_writed_size:0 rdb_parsed_size:0 rdb_parsed_begin:0 rdb_parsed_time:0 #replication master_replid:d3e707ec0e72c3908b0ce70dd2460f48086c5386 repl_offset:683087907631 write_command_count:0 finish_command_count:0 last_replack_time:0 #queue send_write_pos:0 send_read_pos:0 response_write_pos:0 response_read_pos:0 errtime:1654369638 errmsg:Error reading bulk length while SYNCing:Operation now in progress read rdb length from src fail save rdb fail ready shutdown dts
```

### Solution
Disconnect the source database and adjust the limit on the connections to the source system kernel.
```
echo "net.ipv4.tcp_max_syn_backlog=4096" >> /etc/sysctl.conf
echo "net.core.somaxconn=4096" >> /etc/sysctl.conf
echo "net.ipv4.tcp_abort_on_overflow=0" /etc/sysctl.conf
sysctl -p
```

## Issue 6
### Description
The following error message is displayed during migration from Redis Memory Edition (Standard Architecture) to Cluster Architecture with DTS:
```
[launch]state:8 #rdb rdbfile:./tmp1645683629_34614.rdb rdbsize:781035471 rdb_writed_size:781035471 rdb_parsed_size:781035471 rdb_parsed_begin:1645683632 rdb_parsed_time:25 #replication master_replid:5abe7987b1e263582c68835412d2963eeb0a3d60 repl_offset:895807918761 write_command_count:6102523 finish_command_count:6102137 last_replack_time:1645683656 #queue send_write_pos:101832 send_read_pos:101742 response_write_pos:101742 response_read_pos:101357 errtime:1645683657 errmsg:get rsp error:CROSSSLOT Keys in request don't hash to the same slot command:*3 $6 RENAME $16 dispatch:km:pool $34 dispatch:km:tmp-pool:1645683651224 ready shutdown dts send replconf ack to src fail:Bad file descriptor
```

### Cause
The database involves multi-key, transactional, or cross-slot operations. For more information, see [Check on Migration from Standard Architecture to Cluster Architecture](https://intl.cloud.tencent.com/document/product/239/37594).

### Solution
Migrate the data to a Standard Architecture instance in the cloud, or change the business logic to clear multi-key operations.

## Issue 7
### Description
The following error message is displayed during migration with DTS:
```
[launch]state:7 #rdb rdbfile:./tmp1633836033_79441.rdb rdbsize:1008499748 rdb_writed_size:1008499748 rdb_parsed_size:607311937 rdb_parsed_begin:1633836038 rdb_parsed_time:0 #replication master_replid:d42935b9537b1d76ddd9e99e7cb8d4bc22a3e0c3 repl_offset:4649070152868 write_command_count:1569934 finish_command_count:1546843 last_replack_time:1633836088 #queue send_write_pos:69933 send_read_pos:69934 response_write_pos:69934 response_read_pos:46843 errtime:1633836089 errmsg:send replconf ack to src fail:Connection reset by peer rdb parse error: Wrong RDB checksum rdb load fail ready shutdown dts
```

You can see the following information in the execution log of the source node:
```
44:M 05 Jun 03:31:06.728 * Starting BGSAVE for SYNC with target: disk
44:M 05 Jun 03:31:06.978 * Background saving started by pid 89
89:C 05 Jun 03:32:08.417 # Error moving temp DB file temp-89.rdb on the final destination 20617.20324.rdb (in server root dir /opt/data/dump): No such file or directory
44:M 05 Jun 03:32:08.698 # Background saving error
44:M 05 Jun 03:32:08.698 # Connection with slave 10.xx.xx.119:<unknown-slave-port> lost.
44:M 05 Jun 03:32:08.698 # SYNC failed. BGSAVE child returned an error
44:M 05 Jun 03:50:24.626 * Slave 10.xx.xx.119:<unknown-slave-port> asks for synchronization
44:M 05 Jun 03:50:24.626 * Full resync requested by slave 10.xx.xx.119:<unknown-slave-port>
44:M 05 Jun 03:50:24.626 * Starting BGSAVE for SYNC with target: disk
44:M 05 Jun 03:50:24.880 * Background saving started by pid 90
90:C 05 Jun 03:51:22.585 * DB saved on disk
90:C 05 Jun 03:51:22.739 * RDB: 280 MB of memory used by copy-on-write
44:M 05 Jun 03:51:23.008 * Background saving terminated with success
44:M 05 Jun 03:51:27.898 * Synchronization with slave 10.xx.xx.119:<unknown-slave-port> succeeded
44:M 05 Jun 03:52:19.531 # Connection with slave client id #317862457 lost.
```

### Cause
This is often because the connection of the DTS task to the source node timed out due to network environment issues, big keys contained in the database, or `client-output-buffer-limit` overflows on the source node.

### Solution
- Check the source network environment for any issue. For detailed directions, see [Database Connection Check](https://intl.cloud.tencent.com/document/product/571/42552).
- Clear big keys in the source database. You can quickly locate, assess, and delete big keys as instructed in [Memory Analysis](https://intl.cloud.tencent.com/document/product/239/47576).
- Run the following command to set the `client-output-buffer-limit` to infinite on the source node.
```
config set client-output-buffer-limit 'slave 0 0 0' 
```

## Issue 8
### Description
The following error message is displayed during migration with DTS:
```
[launch]state:7 #rdb rdbfile:./tmp1654365384_70581.rdb rdbsize:1664871634 rdb_writed_size:1664871634 rdb_parsed_size:1266531 rdb_parsed_begin:1654365387 rdb_parsed_time:0 #replication master_replid:d3e707ec0e72c3908b0ce70dd2460f48086c5386 repl_offset:683001122815 write_command_count:17818 finish_command_count:11224 last_replack_time:0 #queue send_write_pos:30251 send_read_pos:17767 response_write_pos:17767 response_read_pos:11213 errtime:1654365387 errmsg:rdb parse error: Short read or OOM loading DB. Unrecoverable error rdb load fail ready shutdown dts
```

### Cause
If this error message is displayed when you retry a failed DTS task, it generally indicates that the target node is not empty or the memory is full.

### Solution
Clear the target node and try again, or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for DTS overwrite.

## Issue 9
### Description
The following error message is displayed during migration with DTS:
```
[launch]state:8 #rdb rdbfile:./tmp1653290250_19158.rdb rdbsize:1721160435 rdb_writed_size:1721160435 rdb_parsed_size:1721160435 rdb_parsed_begin:1653290255 rdb_parsed_time:124 #replication master_replid:ed87c56060bc5f9b28da6d7ef2f83a15d56a4827 repl_offset:239048673513 write_command_count:360526495 finish_command_count:360520725 last_replack_time:1654350624 #queue send_write_pos:406694 send_read_pos:406694 response_write_pos:406694 response_read_pos:400925 errtime:1654350625 errmsg:redisBufferRead read rsp from target fail:1:Connection reset by peer ready shutdown dts send replconf ack to src fail:Bad file descriptor
```

### Cause
The Redis node of the target instance experienced an HA master/replica switch, or the proxy node experienced a failover, causing the sync task to fail.

### Solution
Create a new DTS task and configure the new node after the HA switch as the target node for data migration.

## Issue 10
### Description
When the memory eviction policy of the target instance is set to `allkey-lru` during migration with DTS, the following error message is displayed:
```
[launch]state:8 #rdb rdbfile:./tmp1638263556_29975.rdb rdbsize:597343276 rdb_writed_size:597343276 rdb_parsed_size:428299275 rdb_parsed_begin:1638263575 rdb_parsed_time:7 #replication master_replid:ae0dfc45f72f3ee8642c8e31e493b6442179734f repl_offset:34832262785 write_command_count:6811 finish_command_count:6798 last_replack_time:1638263582 #queue send_write_pos:6811 send_read_pos:6811 response_write_pos:6811 response_read_pos:6799 errtime:1638263583 errmsg:get rsp error:OOM command not allowed when used memory > 'maxmemory'. command:*3 $3 SET $26 all_business_newmikoxmsong $1189783 [{"id":3,"label":"AI\u5e73\u53f0\u90e8","node_level":0,"leaf":false,"children":[{"id":"887381","label":"[OMG][\u4f53\u80b2\u641c\u7d22][CMDB]","node_level":1,"leaf":false,"children":[{"id":"722605","label":"[\u4e2a\u6027\u5316\u63a8\u8350\u4e2d\u5fc3][\u817e\u8baf\u7f51\u4f53\u80b2APP\u63a8\u8350]","node_level":2,"leaf":false,"children":[],"collet":0}],"collet":0},{"id":"460871","label":"[OMG][\u817e\u8baf\u89c6\u9891\u641c\u7d22][CMDB]","node_level":1,"leaf":false,"children":[{"id":"383393","label":"[\u641c\u7d22\u4e1a\u52a1\u4e2d\u5fc3][\u817e\u8baf\u89c6\u9891\u641c\u7d22]","node_level":2,"leaf":false,"children":[],"collet":0}],"collet":0}]},{"id":8,"label":"IDC\u5e73\u53f0\u90e8","node_level":0,"leaf":false,"children":[{"id":"452519","label":"IDC\u5e73\u53f0\u90e8\u81ea\u7528[CMDB]","node_level":1,"leaf":false,"children":[{"id":"453099","label":"IDC\u7cfb\u7edf\u5f00\u53d1","node_level":2,"leaf":false,"children":[],"collet":0}],"collet":0}]},{"id":14 ready shutdown dts send replconf ack to src fail:Bad file descriptor
```

### Cause
The memory of the target instance is smaller than the memory used by the data to be migrated from the source database. 

### Solution
Expand the memory of the target instance and then initiate a new DTS migration task. For detailed directions, see [Changing Instance Specification](https://intl.cloud.tencent.com/document/product/239/31934).

## Issue 11
### Description
The following error message is displayed during migration with DTS:
![](https://qcloudimg.tencent-cloud.cn/raw/adeb52bc4cde209a3d896ecd7557a940.png)

### Cause
If an error is reported when you start a DTS migration task with a proxy, it is usually because the bandwidth of the proxy is insufficient.

### Solution
Expand the bandwidth of the proxy or perform migration tasks serially in sequence. For detailed directions, see [Bandwidth Adjustment](https://intl.cloud.tencent.com/document/product/239/46560).

## Issue 12
### Description
The following error message is displayed during migration with DTS:
```
[launch]SrcInstance nodes has changed.
```

### Cause
The source node experienced an HA master/replica switch, causing the DTS task sync to fail.

### Solution
Create a new DTS task and configure the new node after the HA switch as the target node for data migration.


