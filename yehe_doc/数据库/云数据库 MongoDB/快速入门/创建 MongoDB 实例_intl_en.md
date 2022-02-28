The TencentDB for MongoDB console makes working with database instances simple without having to write code or run programs. 

## Prerequisites
You have registered a Tencent Cloud account and completed identity verification.

- To register a Tencent Cloud account:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Click here to sign up for a Tencent Cloud account</a></div>

- To verify your identity:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Click here to verify your identity</a></div>

## Directions
1. Log in to the [TencentDB for MongoDB purchase page](https://buy.intl.cloud.tencent.com/mongodb) with a Tencent Cloud account.
2. Specify instance configurations as needed. Required configuration items are as follows.
<table class="table-striped">
<tbody>
<tr><th>Configuration Item</th><th>Description</th></tr>
<tr>
<td>Billing Mode</td>
<td><b>Pay-as-You-Go</b> is supported. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/3550">Billing Overview</a>.</td></tr>	
<tr>
<td>Region</td>
<td>Select a region where your instance resides. Please select a region closest to you to reduce access latency.<ul><li>Note that the region cannot be changed after the instance is successfully created.</li><li>We recommend that you select the same region as the CVM instance for private network communication.</li></ul></td></tr>
<tr>
<td>AZ</td>
<td>Both single-AZ and multi-AZ deployment schemes are supported.<ul><li>Select an AZ in the region where the instance resides.</li><li>If you select <b>multi-AZ deployment</b>, select AZs for the <b>primary node</b>, <b>secondary node 1</b>, and <b>secondary node 2</b>. To ensure successful cross-AZ switch, <b>multi-AZ deployment</b> only supports deploying instance nodes to three AZs.</li></ul></td></tr>	
<tr>
<td>Configuration Type</td>
<td>Select the configuration type of the instance. <b>Ten-Gigabit High IO</b> is selected by default.</td></tr>
<tr>
<td>Version</td>
<td>Select the database version. MongoDB <b>4.2</b>, <b>4.0</b>, <b>3.6</b>, and <b>3.2</b> are supported. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/31706">Storage Engine and Version</a>.</td></tr>
<tr>
<td>Engine</td>
<td>The default storage engine is <b>WiredTiger</b>. Only MongoDB 3.2 supports <b>Rocks</b>. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/31706">Storage Engine and Version</a>.</td></tr>
<tr>
<td>Instance Type</td>
<td>Select the instance architecture. <b>Replica set</b> and <b>sharded cluster</b> are supported. For more information, see <a href="https://cloud.tencent.com/document/product/240/64126">System Architecture</a>.<ul><li>For a replica set instance, the one-primary-two-secondary architecture is adopted by default.</li><li>For a sharded cluster instance, you need to specify <b>the number of shards</b> and <b>the number of nodes per shard</b>.</li></ul></td></tr>
<tr>
<td>Shard Quantity</td>
<td>Set the number of shards for a sharded cluster instance. Value range: [2,20]. The more the shards, the larger the cluster storage capacity.</td></tr> 
<tr>    
<td>Nodes per Shard</td>
<td>Set the number of nodes per shard for a sharded cluster instance. By default, each shard has one primary node and two secondary nodes, which currently cannot be modified.</td></tr>
<tr>
<td>mongos Specs</td>
<td>You can select the mongos specification for a MongoDB 4.2 sharded cluster instance.</td></tr>
<tr>
<td>mongos Quantity</td>
<td>You can set the number of mongos for a MongoDB 4.2 sharded cluster instance. Value range: [3,32].</td></tr>
<tr>
<td>configServer Specs</td>
<td>For a MongoDB 4.2 sharded cluster instance, the default specification of configServer is 1 core, 2 GB memory, 20 GB storage, and three replicas, which cannot be modified.</td></tr>
<tr>
<td>configServer Storage</td>
<td>For a MongoDB 4.2 sharded cluster instance, the default specification of configServer is 1 core, 2 GB memory, 20 GB storage, and three replicas, which cannot be modified.</td></tr>
<tr>
<td>mongod Specs</td>
<td>Select the computing specification for your database instance. For available computing specifications, see <a href="https://intl.cloud.tencent.com/document/product/240/3550">Billing Overview</a>.</td></tr> 
<tr>
<td>Capacity</td>
<td>Select storage capacity for your database instance based on the computing specification you selected. By default, the storage space for oplog is 10% of the total storage capacity you selected. You can adjust the oplog size in the console.</td></tr>
<tr>
<td>Network</td>
<td>Both <b>VPC (recommended)</b> and <b>classic network</b> are supported. If you select the private network, only devices in the selected subnet can access the database instance. If you select the classic network, only devices in the selected classic network can access the database instance. If you need new networks, you can create <b>VPCs</b> or <b>subnets</b>.</td></tr>
<tr>
<td>IP Version</td>
<td>IPv6 address access is currently not supported.</td></tr>
<tr>
<td>Project</td>
<td>Assign your instance to a project for easy management.</td></tr>
<tr>
<td>Tag</td>
<td>Add tags to your instance for easy classification and management. Click <b>Add</b> to select tag keys and values.</td></tr>  
<tr>
<td>Instance Name</td>
<td>You can select <b>Set After Creation</b> or <b>Set Now</b>. <br>The instance name can contain up to 60 letters, digits, or symbols (-_).</td></tr>  
<tr>
<td>Set Password</td>
<td><b>Set Now</b> is selected by default.</td></tr>   
<tr>
<td>Username</td>
<td>Default instance username. In MongoDB 3.2, `rwuser` and `mongouser` are the default users. In versions later than MongoDB 3.2, `mongouser` is the default user. After the instance is created, you can create custom accounts.</td></tr>  
<tr>
<td>Password</td>
<td>Set a password for the default instance user. Required password strength: <ul><li>It must contain 8-32 characters. </li><li>It supports uppercase letters, lowercase letters, and digits. </li><li>It supports the following symbols: !@#%^*()_ </li><li>It cannot all be letters or digits.</li></ul></td></tr> 
<tr>
<td>Confirm Password</td>
<td>Enter your password again.</td></tr>  
<tr>
<td>Security Group</td>
<td>Set security group rules to control the inbound/outbound traffic to/from your instance. You can either select a security group from the <b>Existing Security Groups</b> drop-down list or click <b>Custom Security Groups</b> to create one and set <b>inbound</b>/<b>outbound</b> rules. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/12452">Security Group</a>.</td></tr> 
<tr>
<td>Quantity</td>
<td>You can purchase up to 30 instances in each region and up to 10 instances each time.</td></tr>
</tbody></table>

3. Click **Billing Details** to view product pricing and confirm the total fees.
4. Click **Buy Now**. After the purchase success message is displayed, click **Go to Console** to enter the instance list page. After the instance's status becomes **Running**, you can use it.

## API
For more information on how to create TencentDB instances via the API, see [CreateDBInstanceHour](https://intl.cloud.tencent.com/document/product/240/34704).

