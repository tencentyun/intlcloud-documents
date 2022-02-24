## Creating Cluster
1. Log in to the [Cloud Data Warehouse overview page](https://intl.cloud.tencent.com/product/cdwch) and click **Buy Now** or log in to the [Cloud Data Warehouse console](https://console.cloud.tencent.com/cdwch) and click **New Cluster** with your Tencent Cloud account.
2. On the purchase page, configure and purchase a cluster as prompted. For more information on configuration items, see [Configuration Items](#jump).
![](https://qcloudimg.tencent-cloud.cn/raw/5de5d6bb0689480d21568217d356f8bb.png)
[](id:jump)
#### Configuration items
<table>
<thead>
<tr>
<th>Configuration Item</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Billing Mode</td>
<td><ul><li/>Monthly subscription: <a href="https://intl.cloud.tencent.com/document/product/555/42701" target="_blank">prepaid</a>, where you should make a payment before creating clusters and using resources.<li/>Pay-as-you-go: <a href="https://intl.cloud.tencent.com/document/product/555/30328" target="_blank">postpaid</a>, where a bill is generated hourly based on resource usage and then you pay for what you use.</ul></td>
</tr>
<tr>
<td>Region</td>
<td>Currently, Cloud Data Warehouse is available in the Shanghai, Hong Kong (China), Beijing, Guangzhou, Singapore, and Silicon Valley regions. We recommend you select a region closest to your users, and you cannot change the region after the purchase.</td>
</tr>
<tr>
<td>Availability Zone</td>
<td>Select availability zones in different regions as needed on the purchase page.</td>
</tr>
<tr>
<td>Network</td>
<td>A VPC is an isolated, highly secure, and dedicated network environment. You can create a VPC and subnet or select an existing one.</td>
</tr>
<tr>
<td>High Availability</td>
<td>In HA mode, each shard has two replicas; in non-HA mode, each shard has only one replica, where the entire cluster will fail if the replica fails. Therefore, we recommend you use the HA mode for production environments.</td>
</tr>
<tr>
<td>Compute Node Type</td>
<td>There are three types of compute nodes:<ul><li>Standard: 4-core 16 GB, 8-core 32 GB, 16-core 64 GB, 24-core 96 GB, 32-core 128 GB, 64-core 256 GB, 90-core 224 GB, and 128-core 256 GB.</li><li>Storage-Optimized: 32-core 128 GB (with twelve 3720 GB SATA HDDs) and 64-core 256 GB (with twenty-four 3720 GB SATA HDDs), 84-core 320 GB (with twenty-four 3720 GB SATA HDDs).</li><li>High-Performance: 32-core 128 GB (with two 3570 GB NVMe SSDs), 64-core 256 GB (with four 3570 GB NVMe SSDs), and 84-core 320 GB (with four 3570 GB NVMe SSDs).</ul><strong>The higher the specification, the better the performance. You can select an appropriate specification as needed.</strong></li></td>
</tr>
<tr>
<td>ZooKeeper Node Type</td>
<td>There are 4-core 16 GB, 8-core 32 GB, 16-core 64 GB, 24-core 96 GB, 32-core 128 GB, 64-core 256 GB, 90-core 224 GB, and 128-core 256 GB ZooKeeper nodes. The heavier the load, the higher the specification needed. You can select an appropriate specification as needed.</td>
</tr>
</tbody></table>

>!You can enable dedicated Grafana monitoring, cluster logging, tiered storage of hot/cold data, and auto-renewal features as needed.




## Viewing Cluster Information
After the cluster is created, go to the [Cloud Data Warehouse console](https://console.cloud.tencent.com/cdwch), select the region where the cluster resides, and view the cluster status and information as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/d71e07e64964fad24f33c39f92b273d8.png)

## Using ClickHouse
Import a data file to a ClickHouse cluster and view the imported data. Prepare the following `account.csv` file:
```
AccountId, Name, Address, Year
1, 'GHua', 'WuHan Hubei', 1990
2, 'SLiu', 'ShenZhen Guangzhou', 1991
3, 'JPong', 'Chengdu Sichuan', 1992
```

### Connecting to cluster
1. [Download](https://repo.yandex.ru/clickhouse/rpm/stable/x86_64/) a ClickHouse client.
```
wget https://repo.yandex.ru/clickhouse/rpm/stable/x86_64/clickhouse-client-20.7.2.30-2.noarch.rpm
wget https://repo.yandex.ru/clickhouse/rpm/stable/x86_64/clickhouse-common-static-20.7.2.30-2.x86_64.rpm
```
- Install the client.
```
rpm -ivh *.rpm
```
- Access the cluster from the client.
 - View the node IP address in the console and select the TCP port `9000`.
```
clickhouse-client -hxxx.xxx.xxx.xxx --port 9000
```
![](https://main.qcloudimg.com/raw/0c8735a3e3b0c62c0b4eacbe4bf143a3.png)
 - Select the HTTP port `8123` and get the specific access IP address in **Cluster Access Address (HTTP)** on the cluster details page.
    - Query and confirm the engine version of the cluster.
```
echo "select version()=21.3.9.83"  |  curl  'http://xxx.xxx.xxx.xxx:8123/' --data-binary @-
```
```
echo "select version()"  |  curl  'http://xxx.xxx.xxx.xxx:8123/' --data-binary @-
```
![](https://main.qcloudimg.com/raw/bfeca4772ca54f4cab73c990f775af54.png)
    - Query the system cluster.
```
echo "select * from system.clusters"  |  curl  'http://xxx.xxx.xxx.xxx:8123/' --data-binary @-
```
![](https://main.qcloudimg.com/raw/7af6c5a3fde244f1a23c7543f3fa5f18.png)


### Creating data table
Use the ClickHouse client to connect to the cluster and create databases and tables.
- Create a database in HA mode
```
CREATE DATABASE IF NOT EXISTS testdb ON CLUSTER default_cluster;
```
![](https://main.qcloudimg.com/raw/431edf9f37809a6f3291ade31ab66f88.png)
- Create a table in HA mode
```
CREATE TABLE testdb.account ON CLUSTER default_cluster(accountid UInt16,name String,address String,year UInt64) ENGINE =ReplicatedMergeTree('/clickhouse/tables/{layer}-{shard}/testdb/account', '{replica}') ORDER BY (accountid);
```
![](https://main.qcloudimg.com/raw/191c2583f53c1a9239cdbeb1e2bff3d1.png)
- Create a database in non-HA mode
```
CREATE DATABASE IF NOT EXISTS testdb ON CLUSTER default_cluster;
```
![](https://main.qcloudimg.com/raw/b7c4bd73b0828c0bc5e368ba4d9c8a85.png)
- Create a table in non-HA mode
```
CREATE TABLE testdb.account ON CLUSTER default_cluster(accountid UInt16, name String, address String, year UInt64) ENGINE =MergeTree() ORDER BY (accountid);
```
![](https://main.qcloudimg.com/raw/c2648404720241637824f8593a05db0c.png)

### Importing data
Place the prepared data in the `/data` directory of the CVM instance connected to the ClickHouse cluster and run the following command to import the data.
```
cat /data/account.csv | clickhouse-client - hxxx.xxx.xxx.xxx --database=testdb --query="INSERT INTO account FORMAT CSVWithNames"
```

### Querying data
```
select * from testdb.account;
```
![](https://main.qcloudimg.com/raw/a450aded73e9e367e61e3bd6ba456e31.png)
