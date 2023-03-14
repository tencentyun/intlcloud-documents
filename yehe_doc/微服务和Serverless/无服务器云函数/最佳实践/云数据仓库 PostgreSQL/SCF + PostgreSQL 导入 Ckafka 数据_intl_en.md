## Overview
This document introduces a free-of-maintenance approach to import Kafka data to Cloud Data Warehouse PostgreSQL instances by using SCF. 

Cloud Data Warehouse PostgreSQL (CDWPG) can sync messages from the messaging middleware for analysis. 

## Limits
- Only Tencent Cloud CKafka is supported as the data source. External Kafka services are not supported.
- One function can only import data to one table in CDWPG. To write data into multiple tables, you need to create one function for each table.

## Directions
### Step 1. Create a function
In the [SCF console](https://console.cloud.tencent.com/scf/index?rid=4), select **Functions > Create**. In the **Create** page, enter **ckafka** and **CDW** in the **Fuzzy search** field, complete the settings and click **Next**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/D5QU540_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221230164750.png)
On the **Function configuration** page, complete the settings in **Environment configuration** and **Network configuration** in **Advanced configuration** as follows:

- **Environment configuration**
 - Memory: Set the memory based on the actual running status, which is 128 MB by default. If it is insufficient during data import, you should increase it.
 - Environment variable:
<table>
	<thead>
	<tr>
	<th>Parameter</th>
	<th>Required</th>
	<th>Description</th>
	</tr>
	</thead>
<tbody>
	<tr>
		<td>DB_DATABASE</td>
		<td>Supported</td>
		<td>Database name</td>
	</tr>
	<tr>
		<td>DB_HOST</td>
		<td>Supported</td>
		<td>If the function is deployed in a VPC and in the same subnet as CDWPG, you can enter the private IP of CDWPG; otherwise, enter the public IP and configure an allowlist.</td>
	</tr>
	<tr>
		<td>DB_USER</td>
		<td>Supported</td>
		<td>Username</td>
	</tr>
	<tr>
		<td>DB_PASSWORD</td>
		<td>Supported</td>
		<td>User password</td>
	</tr>
	<tr>
		<td>DB_SCHEMA</td>
		<td>Supported</td>
		<td>Schema name. If it is not specified during table creation, it will be `public` in general.</td>
	</tr>
	<tr>
		<td>DB_TABLE</td>
		<td>Supported</td>
		<td>Table name</td>
	</tr>
	<tr>
		<td>DB_PORT</td>
		<td>No</td>
		<td>CDWPG port, which is 5436 by default.</td>
	</tr>
	<tr>
		<td>MSG_SEPARATOR_ASCII</td>
		<td>No</td>
		<td>ASCII code of the data delimiter in CKafka, which is 39 (comma) by default. As commas usually show up in the business data, we recommend you set this parameter to 11 (vertical bar).</td>
	</tr>
	<tr>
		<td>MSG_NULL</td>
		<td>No</td>
		<td>NULL value of CKafka consumption. The default value is `\N`</td>
	</tr>
	<tr>
		<td>REPLACE_0X00</td>
		<td>No</td>
		<td>Whether to replace "0x00" in strings. The default value is 0 (1 indicates to replace).</td>
	</tr>
	<tr>
		<td>ENABLE_DEBUG</td>
		<td>No</td>
		<td>Whether to print error records. The default value is 0 (1 indicates to print).</td>
	</tr>
	<tr>
		<td>ENABLE_COS</td>
		<td>No</td>
		<td>Whether to dump unwritten records to COS. The default value is 0 (1 indicates to dump).</td>
	</tr>	
	<tr>
		<td>COS_SECRET_ID</td>
		<td>No</td>
		<td>`secret_id` for COS access. If `ENABLE_COS` is 1, this field is required.</td>
	</tr>	
	<tr>
		<td>COS_SECRET_KEY</td>
		<td>No</td>
		<td>`secret_key` for COS access. If `ENABLE_COS` is 1, this field is required.</td>
	</tr>	
	<tr>
		<td>COS_BUCKET</td>
		<td>No</td>
		<td>COS bucket name. If `ENABLE_COS` is 1, this field is required.</td>
	</tr>	
	<tr>
		<td>STATMENT_TIMEOUT</td>
		<td>No</td>
		<td>Query timeout period, which is 50 seconds by default.</td>
	</tr>	
</tbody>
</table>
- **Network configuration**
 - VPC: **Activate** VPC and set the same VPC and subnet values as those of the CDWPG instance.
 ![](https://qcloudimg.tencent-cloud.cn/raw/b8d7e97e7d4a61c2b81ce772d5b183c4.png)
 The corresponding values in CDWPG are as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/fR4z323_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221230164903.png)
 - Public Network Access: **Enable** 

### Step 2. Configure a trigger

In the **Functions** list in the [SCF console](https://console.cloud.tencent.com/scf/index?rid=4), click the name of the newly created function to enter the function details page and click **Trigger management** > **Create trigger** on the left to create a trigger. Here, set **CKafka trigger** for **Trigger method**.
![](https://qcloudimg.tencent-cloud.cn/raw/01a053c7cea01dc919664c0bf2bda09f.png)

For details of trigger settings, see [CKafka Trigger Description](https://intl.cloud.tencent.com/document/product/583/17530).


