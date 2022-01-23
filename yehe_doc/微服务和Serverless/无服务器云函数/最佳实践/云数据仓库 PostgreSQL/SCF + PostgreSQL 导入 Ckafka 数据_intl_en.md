## Background
SCF provides a serverless execution environment for companies and developers. For more information, see [SCF](https://intl.cloud.tencent.com/zh/product/scf).

A common use case of CDWPG is to syncing messages from the messaging middleware for analysis. This document describes a convenient method where an SCF function imports data from Kafka to CDWPG in real time, eliminating your need to maintain any services.

## Notes
- This function currently can use CKafka as the data source and does not support self-built Kafka.
- This function currently can write data into only one table in CDWPG as the target. If you want to write data into multiple tables, create the corresponding function for each table as follows:

## Directions
### Step 1. Create a function
In the [SCF console](https://console.cloud.tencent.com/scf/index?rid=4), select **Function Service** > **Create**. On the **Create Function** page, select **Phython3.6** as the **runtime environment**, search for the keyword "ckafka" in **Fuzzy search**, select the template function **Load CKafka Data into CDW**, and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/48f0e533bf7677ee50714b13cd9b5388.png)
On the **Function Configuration** page, complete the settings in **Environment Configuration** and **Network Configuration** in **Advanced Configuration** as follows:

- **Environment Configuration**
 - Memory: set the memory based on the actual running status, which is 128 MB by default. If it is insufficient during data import, you should increase it.
 - Environment variables:
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
		<td>Yes</td>
		<td>Database name.</td>
	</tr>
	<tr>
		<td>DB_HOST</td>
		<td>Yes</td>
		<td>If the function is deployed in a VPC and in the same subnet as CDWPG, you can enter the private IP of CDWPG; otherwise, enter the public IP and configure an allowlist.</td>
	</tr>
	<tr>
		<td>DB_USER</td>
		<td>Yes</td>
		<td>Username.</td>
	</tr>
	<tr>
		<td>DB_PASSWORD</td>
		<td>Yes</td>
		<td>User password.</td>
	</tr>
	<tr>
		<td>DB_SCHEMA</td>
		<td>Yes</td>
		<td>Schema name. If it is not specified during table creation, it will be `public` in general.</td>
	</tr>
	<tr>
		<td>DB_TABLE</td>
		<td>Yes</td>
		<td>Table name.</td>
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
- **Network Configuration**
 - VPC: we recommend you **activate** VPC and set the same VPC and subnet values as those of the CDWPG instance.
 ![](https://qcloudimg.tencent-cloud.cn/raw/b8d7e97e7d4a61c2b81ce772d5b183c4.png)
    The corresponding values in CDWPG are as shown below:
 - Public Network Access: we recommend you also **enable** this option.

### Step 2. Configure a trigger

In the **Function Service** list in the [SCF console](https://console.cloud.tencent.com/scf/index?rid=4), click the name of the newly created function to enter the function details page and click **Trigger Management** > **Create a Trigger** on the left to create a trigger. Here, set **CKafka trigger** for **Trigger Method** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/01a053c7cea01dc919664c0bf2bda09f.png)

For more information on trigger parameter configuration, see [CKafka Trigger Description](https://intl.cloud.tencent.com/document/product/583/17530).
