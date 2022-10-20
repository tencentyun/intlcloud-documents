## Overview

The TencentDB for MongoDB console makes it simple to work with database instances without writing code or running programs. This document describes how to purchase and configure a TencentDB for MongoDB instance as described in [Viewing Instance Details](https://intl.cloud.tencent.com/document/product/240/44179). 

## Prerequisites
- You have registered a Tencent Cloud account and completed identity verification.
  - To register a Tencent Cloud account:
    
    <div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Click here to sign up for a Tencent Cloud account</a></div>
  - To complete identity verification:
    
    <div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Click here to verify your identity</a></div>
- You have determined a region and AZ for the instance. For more information, see [Regions and AZs](https://intl.cloud.tencent.com/document/product/240/3637).
- You have determined the specification and performance requirements of the instance. For more information, see [Product Specifications](https://intl.cloud.tencent.com/document/product/240/31183) and [Performance](https://intl.cloud.tencent.com/document/product/240/46145).
- You have determined a VPC and security group for the instance. For more information, see [Creating VPC](https://intl.cloud.tencent.com/document/product/215/31805) and [Configuring Security Group](https://intl.cloud.tencent.com/document/product/240/31489). Currently, access over the public network isn't supported.
- You have checked out the billing details of the instance. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/240/3550). Database fees for one hour will be frozen when you create a pay-as-you-go database. Make sure that your account balance is sufficient before making a purchase.
- You have determined the business project of the instance. You can create a project in **Project Management** in the **Account Center**.
- You have understood the differences between each database versions. For more information, see [Storage Engine and Version](https://intl.cloud.tencent.com/document/product/240/31706).

## Directions

1. Log in to the [TencentDB for MongoDB purchase page](https://buy.intl.cloud.tencent.com/mongodb) with a Tencent Cloud account.
2. Specify instance configurations as needed. Required configuration items are as follows.
<table class="table-striped">
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Billing Mode</td>
<td><b>Pay-as-you-go</b> is supported. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/3550">Billing Overview</a>.</td></tr>	
<tr>
<td>Region</td>
<td>Select a region where your instance resides. You should select a region closest to you to reduce access latency.<ul><li>Note that the region cannot be changed after the instance is successfully created.</li><li>We recommend you select the same region as the CVM instance for private network communication.</ul></td></tr>
<tr>
<td>Database Version</td>
<td>Select a database version from <b>4.4</b>, <b>4.2</b>, <b>4.0</b>, <b>3.6</b>, and <b>3.2</b>. Currently, v3.2 is no longer for sales. We recommend you select a later version. For more information on how to select an appropriate version, see the version description in <a href="https://intl.cloud.tencent.com/document/product/240/31706">Storage Engine and Version</a>. After purchasing an instance, you can upgrade its version as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/47677">Version Upgrade</a>.</td></tr>
<tr>
<td>Architecture Type</td>
<td>Select a system architecture for the instance cluster. Supported architectures include <b>replica set</b>, <b>sharded cluster</b>, and <b>single-node</b>. The single-node architecture is no longer for sales. You need to understand the use cases of different architectures and select an appropriate one based on the actual data volume of your business. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/44173">System Architecture</a>. Currently, architecture upgrade isn't supported.</li></ul></td></tr>    
<tr>
<td>Storage Engine</td>
<td>The default storage engine is <b>WiredTiger</b>.</td></tr>
<tr>
<td>Mongod Specification</td>
<td>Select the computing specification of the instance from the drop-down list. The higher the specification, the higher the IOPS. For supported specifications, see <a href="https://intl.cloud.tencent.com/document/product/240/31183">Product Specifications</a>. After creating an instance, you can adjust its computing specification as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/31192">Adjusting Instance Specification</a>.</td></tr> 
<tr>
<td>Mongod Shard Quantity</td>
<td>This parameter will be displayed if you select <b>Sharded Cluster</b> for <b>Architecture Type</b>. It is used to set the mongod shard quantity in a sharded cluster instance, and its value range is [1,20]. Each shard is a replica set. The more the shards, the larger the cluster storage capacity. You can select a shard quantity as needed. After creating an instance, you can adjust the shard quantity as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/31192">Adjusting Instance Specification</a>.</td></tr> 
<tr>
<td>Disk Capacity</td>
<td>Select the storage capacity of the instance on the slider. The range of the disk capacity varies by mongod specification. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/31183">Product Specifications</a>. The default oplog storage space is 10% of the selected storage capacity. You can adjust the oplog capacity in the instance list in the console as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/49158">Adjusting Oplog Capacity</a>. After creating an instance, you can adjust its disk capacity as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/31192">Adjusting Instance Specification</a>.</td></tr>
<tr>    
<td>Number of primary and secondary nodes</td>
<td>This parameter will be displayed if you select <b>Replica Set</b> for <b>Architecture Type</b>. It is one-primary-two-secondary architecture with three storage nodes by default. Currently, you cannot customize the number of secondary nodes. You can select five (one-primary-four-secondary) or seven (one-primary-six-secondary) nodes from the drop-down list. After creating the instance, you can add more secondary nodes per shard as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/49132">Adding Replica Node</a>.</td></tr>
<tr>    
<td>Number of primary and secondary nodes per shard</td>
<td>The number of nodes per shard in a sharded cluster instance. This parameter will be displayed if you select <b>Sharded Cluster</b> for <b>Architecture Type</b>. The system adopts a one-primary-two-secondary architecture with three nodes by default, that is, each shard has three nodes in a in one-primary-two-secondary architecture. You can select five (one-primary-four-secondary) or seven (one-primary-six-secondary) nodes from the drop-down list. Currently, you cannot customize the number of nodes. After creating the instance, you can add more secondary nodes per shard as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/49132">Adding Replica Node</a>.</td></tr>
<tr>
<td>Read-Only Node Count</td>
<td>The number of read-only nodes. You can configure <b>0</b> or <b>1–5 read-only nodes</b>. Currently, only v4.0 and v4.2 support this parameter, while v3.6 doesn't. After creating the instance, you can add more read-only nodes as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/49130">Adding Read-Only Node</a>.</td></tr>
<tr>
<td>Configuration Description</td>
<td>This parameter calculates the maximum number of connections to the instance based on the configured mongod specification to help you determine whether the current specification meets the expectation.</td></tr>
<tr>
<td>Mongos Specification</td>
<td>Mongos specification. This parameter will be displayed if you select <b>Sharded Cluster</b> for <b>Architecture Type</b>. <ul><li>After you configure the mongod specification, the corresponding mongos specification will be selected by default. For example, if you select 2-core 4 GB MEM for mongod, the mongos specification will be configured as 1-core 2 GB MEM by default. After the mongos specification is upgraded, fees will be charged based on the new specification. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/8364">MongoDB Pricing</a>. </li><li>The number of connections to the sharded cluster instance is subject to the selected mongos node specification and quantity. You can view the maximum number of connections of the instance in <b>Configuration Description</b>. </li><li>After creating the instance, you can adjust the mongos specification as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/49128">Adjusting Mongos Node Specification</a>.</li></ul></td></tr>
<tr>
<td>Mongos Quantity</td>
<td>Mongos node quantity. This parameter will be displayed if you select <b>Sharded Cluster</b> for <b>Architecture Type</b>. If the instance is deployed in the same AZ, it can contain 3–32 mongos nodes. If you select <b>Multi-AZ Deployment</b> for <b>AZ</b> to deploy the instance across different AZs, the instance can contain 6–32 mongos nodes.<ul><li>Added mongos nodes will incur fees. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/8364">MongoDB Pricing</a>. </li><li>After creating the instance, you can adjust the mongos node quantity as instructed in <a href="https://intl.cloud.tencent.com/document/product/240/49127">Adding Mongos Node</a>.</li></ul></td></tr>
<tr>
<td>Network</td>
<td>You can select <b>VPC</b> only.</td></tr>
<tr>
<td>AZ</td>
<td>Enable <b>Multi-AZ Deployment</b> as needed. Multi-AZ deployment refers to deploying an instance across different AZs in the same region. Compared with single-AZ deployment, it has a higher availability and disaster recovery capability.<ul><li>If your instance is deployed in the same AZ, select an AZ for the primary node from the drop-down list after <b>Primary Node</b>. </li><li>If your instance is deployed across different AZs, select an AZ for the primary node from the drop-down list after <b>Primary Node</b> and specify the AZ for each secondary node in each drop-down list after **Secondary Node n** (n=1,2,3,4,5,6).</li><li>If the read-only node count is configured, configure the AZ for each read-only node.</li></ul>After creating the instance, you can <a href="https://intl.cloud.tencent.com/document/product/240/44182">modify the instance AZ</a>.</td></tr>
<tr>
<td>IPv4 Network</td>
 <td>You should select a specific VPC and subnet, preferably the same <a href="https://intl.cloud.tencent.com/document/product/215">VPC</a> in the same region as the CVM instance. VPCs are region-specific (e.g., Guangzhou), while subnets are AZ-specific (e.g., Guangzhou Zone 1). One VPC can be divided into one or multiple subnets, which are interconnected over the private network by default. Different VPCs are isolated over the private network by default, no matter whether they are in the same or different regions. You can switch the VPC after instance purchase as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/31944">Configuring Network</a>. You can also click <b>Create VPCs</b> and <b>Create Subnets</b> to create a required network environment as instructed in <a href="https://intl.cloud.tencent.com/document/product/215/31805">Creating VPC</a>.</td></tr>
<tr>
<td>IPv6 Network</td>
<td>Select whether to enable access over IPV6. This feature is not supported currently.</td></tr>
<tr>
<td>Security Group</td>
<td>Set security group rules to control the inbound traffic to your database. You can either select a security group from the <b>Existing Security Groups</b> drop-down list or click <b>Custom Security Groups</b> to create one and set <b>inbound rules</b>. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/12452">Security Group</a>.</td></tr> 
<tr>
<td>Project</td>
<td>Assign your instance to a project for easy management.</td></tr>
<tr>
<td>Tag</td>
<td>Add tags to your instance for easy classification and management. Click <b>Add</b> to select tag keys and values.</td></tr>  
<tr>
<td>Instance Name</td>
<td>Set the instance name. The default name is `500`.<br>You can enter up to 60 letters, digits, hyphens, and underscores.</td></tr>  
<tr>
<td>Set Password</td>
<td>Set the password verification mode of the instance.<ul><li><b>Password Authentication</b>: You need to set an instance password for database access.</li><li><b>Password-Free Access</b>: You don't need to set a password. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/39007">Accessing Instance Without Authentication</a>.</li></ul></td></tr>   
<tr>
<td>Password</td>
<td>The access password of the instance. This parameter will be displayed if you select <b>Password Authentication</b> for <b>Set Password</b>. Required password strength: <ul><li>It must contain 8–32 characters. </li><li>It supports uppercase letters, lowercase letters, and digits. </li><li>It supports the following symbols: !@#%^*()_ </li><li>It cannot all be letters or digits.</li></ul></td></tr> 
<tr>
<td>Confirm Password</td>
<td>Enter your password again.</td></tr>  
<tr>
<td>Quantity</td>
<td>You can purchase up to 30 instances in each region and up to 10 instances each time.</td></tr> 
<tr>
<td>Total Fees</td>
<td><ul><li>Hourly fees will be displayed if you select **Pay as You Go**. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/8364">MongoDB Pricing</a>.</li></ul></td></tr>
</tbody></table>
3. After verifying that the parameters are correctly configured, click **Buy Now**. After the purchase success message is displayed, click **Go to Console**. After the instance's status becomes **Running** in the instance list, you can use it.

## Subsequent operations

- Use a CVM instance to directly access the private network address of the TencentDB instance. For more information, see [Connecting to TencentDB for MongoDB Instance](https://intl.cloud.tencent.com/document/product/240/7092).
- View the instance list and instance details. For more information, see [Viewing Instance Details](https://intl.cloud.tencent.com/document/product/240/44179).

## Related APIs

| API                                                     | Description                     |
| :----------------------------------------------------------- | :--------------------------- |
| [CreateDBInstanceHour](https://intl.cloud.tencent.com/document/product/240/34704) | Creates a pay-as-you-go TencentDB instance. |

