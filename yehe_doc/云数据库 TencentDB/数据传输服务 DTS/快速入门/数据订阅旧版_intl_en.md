DTS provides a binlog-based incremental data subscription feature that allows you to subscribe to incrementally updated data in TencentDB in just a few steps:
1. Purchase and create a subscription channel for your TencentDB instance in the [DTS console](https://console.cloud.tencent.com/dts/dss?rid=1&page=1&pagesize=20).
2. Use the DTS data subscription SDK to connect to this subscription channel to subscribe to and consume incremental data.

## How Subscription Works
Data subscription is implemented by simulating a secondary database to get the corresponding binlog content from the primary database for analysis in the following architecture. While parsing the binlogs and analyzing data according to the database/table configured in the subscription channel, it has almost no impact on the primary database.
![](https://main.qcloudimg.com/raw/683946179562ed3261f8f69e15f2a389.png)

- Currently, the subscribed message content in the past day is retained by default.
- If subscription is made at the instance level, subsequently added databases/tables will also appear in the subscription channel, so there is no need to additionally configure the channel.
- If subscription is made at the database level, subsequently added tables will also appear in the subscription channel, so there is no need to additionally configure the channel. In this scheme, if a new database is added, you need to configure the channel.
- The data subscription service currently supports TencentDB for MySQL 5.6 and 5.7.
- Data subscription does not support views, triggers, and foreign keys.
- The initial configuration of data subscription requires adjustment of the relevant binlog_row_image and binlog_format parameters. After the adjustment, data subscription will automatically kill the existing connections in the instance to make the parameters take effect immediately, and it will also execute flush tables to obtain the table structure of the subscribed data. This may affect your database request. Please assess the impact on your business.

## Directions
### Step 1: Create a data subscription channel
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/dss), select **Data Subscription** on the left sidebar, and click **Create Subscription**.
2. On the pop-up page, select the corresponding configurations and click **Buy Now**.
3. After the service is activated, return to the data subscription list, click **Initialize configurations**, and complete initial configuration for the purchased data subscription channel.
4. On the configuration page, select the source TencentDB instance and click **Next**.
![](https://main.qcloudimg.com/raw/35e57fe036eb66f5f6b679de3ebd2cf0.png)
5. Select your desired data sync type and database/table to be synced.
 - The granularity for subscribed objects divides into database level and table level, i.e., you can choose to subscribe to certain databases or tables.
 - The types of subscribed data include `data update`, `structure update`, and `all`.
 If only data update and subscribed object are selected, you can only subscribe to three types of data changes: `insert`, `delete`, and `update`.
 To subscribe to structure update (DDL), you need to select structure change as the sync type. DTS will pull all structure changes in the entire TencentDB instance, and you need to filter out the desired data by using the SDK.
 If `all` is selected, both data update and structure update will be subscribed to.
![](https://main.qcloudimg.com/raw/92a2e19ad825bcc07ec03fb3258f4cb6.png)
6. After confirming the subscribed object and type, click **Start** to enable the subscription channel.

### Step 2: Modify the consumption starting time point
DTS allows you to modify the consumption starting time point at any time during the consumption process. Once the modification is completed, the downstream SDK will begin pulling incremental data starting from the new starting time point.
>?Currently, DTS only supports modifying the consumption time point in the console. You cannot specify it in the SDK.

The modification steps are as follows:
1. Stop the SDK consumption process.
In the [Data Subscription](https://console.cloud.tencent.com/dts/dss) list, click a subscription ID or **View Subscription Details** in the "Operation" column to enter the subscription details page. If **Consumer Source (IP)** is none, the process has stopped.
2. Modify the consumption starting time point.
In the [Data Subscription](https://console.cloud.tencent.com/dts/dss) list, move the cursor to the consumption starting time point of the subscription and the "Modify consumption start time" icon will appear. Click the icon to enter the modification page.
>?The new consumption starting time point must fall within the data range of the subscription channel.
>
![](https://main.qcloudimg.com/raw/6136783707136c9c186ef5fec6e696bf.png)
3. Restart the SDK consumption process.
After the consumption starting time point is modified, you can restart the local SDK consumption process. Then, the SDK will begin subscribing to incremental data starting from the new time point.

### Step 3: Modify the subscribed object
DTS allows you to dynamically add/delete subscribed objects during the consumption process.
- If a subscribed object is added, the subscription channel will pull its incremental data starting from the current time.
- If a subscribed object is deleted, the SDK will no longer subscribe to its data.

The modification steps are as follows:
1. In the [Data Subscription](https://console.cloud.tencent.com/dts/dss) list, select **More** > **Modify subscribed object** in the "Operation" column to enter the subscription configuration page.
2. On the subscription configuration page, modify the subscribed object and click **Save**.
![](https://main.qcloudimg.com/raw/313fa9d664d86404be47d8832f825422.png)

### Step 4: Use the SDK to consume data
For more information, please see [SDK User Guide](https://intl.cloud.tencent.com/document/product/571/8776).

## Sample Subscriptions
[Pulling changes in a subscribed table to a local file](https://intl.cloud.tencent.com/document/product/571/34107)
[Pulling changes in a subscribed table to Redis](https://intl.cloud.tencent.com/document/product/571/34106)
[Pulling changes in a subscribed table to Kafka ](https://intl.cloud.tencent.com/document/product/571/16856)
