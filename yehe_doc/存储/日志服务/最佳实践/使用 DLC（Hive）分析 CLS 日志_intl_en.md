## Overview
This document describes how to ship logs in CLS to Hive for OLAP computing. You can use the data analysis and computing services provided by Tencent Cloud Data Lake Compute to complete offline log computing and analysis as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/49cfebe438708b45edd6001625b55ab0.png)

## Directions

### Shipping CLS logs to COS

#### Creating a shipping task
1. Log in to the CLS console and select **Shipping Task Management** > **[Ship to COS](https://console.cloud.tencent.com/cls/shipper/cos)** on the left sidebar.
2. On the **Ship to COS** page, click **Add Shipping Configuration**. In the **Ship to COS** pop-up window, create a shipping task.
Pay attention to the following configuration items:
<table>
<thead>
<tr>
<th width="15%"><strong>Configuration Item</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody><tr>
<td>Directory Prefix</td>
<td>Log files will be shipped to the corresponding directory in the COS bucket, which is generally the address of the table location in a data warehouse model.</td>
</tr>
<tr>
<td>Partition Format</td>
<td>A shipping task can automatically partition data by creation time. We recommend you specify the partition format according to the Hive partitioned table format.<br>For example, to partition by day, you can set <code>/dt=%Y%m%d/test</code>. Here, <code>dt=</code> indicates the partitioning field, <code>%Y%m%d</code> indicates the year, month, and day, and <code>test</code> indicates the log file prefix. As the name of a shipped file start with an underscore (<code>(_)</code>) by default, the big data computing engine will ignore such files and cause a failure to find the data. Therefore, you need to add a prefix, and the actual partition directory name will be <code>dt=20220424</code> for example.</td>
</tr>
<tr>
<td>Shipping Interval</td>
<td>You can select 5–15 minutes. We recommend you select <strong>15 minutes, 250 MB</strong>. In this case, the number of files will be lower, and the query performance will be high.</td>
</tr>
<tr>
<td>Shipping Format</td>
<td>The JSON format is recommended.</td>
</tr>
</tbody></table>



#### Viewing the shipping task result

Generally, you can view the log data in the COS console 15 minutes after the shipping task starts. If you set partitioning by day in the `log_data` logset, the directory structure will be as shown below, where specific log files are stored in partition directories.
![](https://qcloudimg.tencent-cloud.cn/raw/8422e00e0d7543384686805199b205db.png)




### Data Lake Compute (Hive) analysis

#### Using Data Lake Compute to create a foreign table and map it to a COS log directory
After log data is shipped to COS, you can use the data exploration feature in the Data Lake Compute console to create a foreign table. For the table creation statement, refer to the following example. **Note that the partitioning field and the `location` field must match the directory structure.**

The Data Lake Compute foreign table creation wizard provides advanced options to infer the data file table structure and quickly and automatically generate SQL statements. As sampled inference is used, you need to further determine whether table fields are appropriate based on the SQL statements. For example, in the sample code below, it is inferred that the `__TIMESTAMP__` field is of `int` type, but maybe the `bigint` type should be used to meet the business requirements.

```sql
CREATE EXTERNAL TABLE IF NOT EXISTS `DataLakeCatalog`.`test`.`log_data` (
  `__FILENAME__` string,
  `__SOURCE__` string,
  `__TIMESTAMP__` bigint,
  `appId` string,
  `caller` string,
  `consumeTime` string,
  `data` string,
  `datacontenttype` string,
  `deliveryStatus` string,
  `errorResponse` string,
  `eventRuleId` string,
  `eventbusId` string,
  `eventbusType` string,
  `id` string,
  `logTime` string,
  `region` string,
  `requestId` string,
  `retryNum` string,
  `source` string,
  `sourceType` string,
  `specversion` string,
  `status` string,
  `subject` string,
  `tags` string,
  `targetId` string,
  `targetSource` string,
  `time` string,
  `type` string,
  `uin` string
) PARTITIONED BY (`dt` string) ROW FORMAT SERDE 'org.apache.hive.hcatalog.data.JsonSerDe' STORED AS TEXTFILE LOCATION 'cosn://coreywei-1253240642/log_data/'
```
- For shipping by partition, `location` must point to the `cosn://coreywei-1253240642/log_data/` directory instead of the `cosn://coreywei-1253240642/log_data/20220423/` directory.
- To use the inference feature, you need to point the directory to the subdirectory of the data file, i.e., `cosn://coreywei-1253240642/log_data/20220423/`. After inference is completed, change `location` in the SQL statement back to `cosn://coreywei-1253240642/log_data/`.
- Appropriate partitioning can improve the performance. However, we recommend you create no more than 10,000 partitions.


#### Adding a partition
You can use a `SELECT` statement to get data from a partitioned table only after adding partitions in the following two ways:

<dx-tabs>
::: Adding historical partitions
This option can load all partition data at a time but is slow, so it is suitable for scenarios where many partitions need to be loaded for the first time.
```sql
msck repair table DataLakeCatalog.test.log_data;
```

:::
::: Adding incremental partitions
After historical partitions are loaded, incremental partitions will be added periodically. For example, you can use this option to add a partition every day.
```sql
alter table DataLakeCatalog.test.log_data add partition(dt='20220424')
```

:::
</dx-tabs>


#### Analyzing data
After adding partitions, you can use Data Lake Compute for data development and analysis.
```sql
select dt,count(1) from `DataLakeCatalog`.`test`.`log_data` group by dt;
```




