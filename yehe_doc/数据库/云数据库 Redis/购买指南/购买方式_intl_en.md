## Overview

This document describes how to purchase and configure a TencentDB for Redis instance in the following two ways:

- Console: You can configure the instance parameters and directly make a purchase in the web console.
- API: You can call the `CreateInstances` API to make a purchase.

## Preparations for Purchase

- You have registered a Tencent Cloud account and completed identity verification.
  - To register a Tencent Cloud account:
    
    <div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Click here to sign up for a Tencent Cloud account</a></div>
  - To verify your identity:
    
    <div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Click here to verify your identity</a></div>
- You have determined a region and AZ for the instance. For more information, see [Regions and AZs](https://intl.cloud.tencent.com/document/product/239/4106).
- You have determined the specification and performance requirements of the instance. For more information, see [Product Series](https://intl.cloud.tencent.com/document/product/239/31959) and [Performance](https://intl.cloud.tencent.com/document/product/239/17952).
- You have determined a VPC and security group for the instance. For more information, see [Virtual Private Cloud](https://intl.cloud.tencent.com/document/product/215) and [Configuring Security Groups for TencentDB](https://intl.cloud.tencent.com/document/product/239/31945).
- To deploy the instance across multiple AZs in the same region, learn more about the architecture of [multi-AZ deployment](https://intl.cloud.tencent.com/document/product/239/39812) first.
- To support read/write separation, learn more about how [read/write separation](https://intl.cloud.tencent.com/document/product/239/33132) is implemented first.
- You have checked out the billing details of the instance. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/239/31954). Database fees for one hour will be frozen when you create a pay-as-you-go database. Make sure that your account balance is sufficient before making a purchase.

## Purchasing in Console

1. Log in to the [TencentDB for Redis purchase page](https://buy.intl.cloud.tencent.com/redis) with your Tencent Cloud account.
2. Configure the instance as needed based on the parameter descriptions below:
   <table class="table-striped">
   <tbody>
   <tr><th>Parameter</th><th>Description</th></tr>
   <tr>
   <td>Billing Mode</td>
   <td><b>Pay-as-you-go</b>. For more information, see <a href="https://intl.cloud.tencent.com/document/product/239/31954">Billing Overview</a>.</td></tr>	
   <tr>
   <td>Region</td>
   <td>Select a region where your instance resides. Please select a region closest to you to reduce access latency.<ul><li>Note that the region cannot be changed after the instance is successfully created.</li><li>We recommend you select the same region as the CVM instance for private network communication.</li></ul></td></tr>
   <tr>
   <td>Instance Edition</td>
   <td>Select the <b>Memory Edition</b>. The CKV Edition is unavailable currently.</td></tr>
   <tr>
   <td>Compatible Version</td>
   <td>Select a high-performance version based on the open-source Redis engine, which is compatible with Redis 6.0, 5.0, 4.0, and 2.8. v2.8 is unavailable currently, and v4.0 or later is recommended. To purchase an instance of Redis v2.8, <a href="https://intl.cloud.tencent.com/document/product/239/31959">submit a ticket</a> for application.</td></tr>	 
   <tr> 
       <td>Architecture</td>
   <td>v4.0 or later supports the standard architecture and cluster architecture, while v2.8 only supports the standard architecture. For more information on the product architecture, see <a href="https://intl.cloud.tencent.com/document/product/239/31959">Memory Edition (Standard Architecture)</a> and <a href="https://intl.cloud.tencent.com/document/product/239/18336">Memory Edition (Cluster Architecture)</a>.</td></tr>
   <tr>
   <td>Memory</td>
   <td>Configure the required memory size (0.25–64 GB) if you select <b>Standard Architecture</b> for <b>Architecture</b>.</td></tr>
   <tr>
   <td>Replica Quantity</td>
   <td>Select the number of database replicas. Multiple replicas can provide master/replica high availability, thus improving the data security. Replicas can also be used to enhance the read-only performance. The replica quantity may vary by region or edition as configured in the console by default.</td></tr>
   <tr>
   <td>Shard Quantity</td>
   <td>Set the number of shards as needed if you select <b>Cluster Architecture</b> for <b>Architecture</b>. The more the shards, the larger the cluster storage capacity.</td></tr> 
   <tr>    
   <td>Shard Capacity</td>
   <td>Set the capacity of each shard if you select <b>Cluster Architecture</b> for <b>Architecture</b>.</td></tr>
   <tr>    
   <td>Specs Preview</td>
   <td>Preview the selected specification and the supported maximum number of connections and maximum network throughput to verify whether they meet your expectations.</td></tr>
   <tr>    
   <td>Read-Only Replica</td>
   <td>Specify whether to enable read/write separation. For more information, see <a href="https://intl.cloud.tencent.com/document/product/239/33132">Read/Write Separation</a>.</td></tr>
   <tr>
   <td>Network</td>
   <td>Both <b>VPC</b> and <b>classic network</b> are supported. If you select VPC, only devices in the selected subnet can access the database instance. If you select the classic network, only devices in the selected classic network can access the database instance, and multi-AZ deployment is not supported.</td></tr>
   <tr>
   <td>AZ</td>
   <td>Specify whether to enable multi-AZ deployment. Both single-AZ deployment and multi-AZ deployment are supported. A multi-AZ deployed instance has higher availability and disaster recovery capabilities than a single-AZ deployed instance. For more information, see <a href="https://intl.cloud.tencent.com/document/product/239/39812">Multi-AZ Deployment</a>. <ul><li>For single-AZ deployment, select an AZ for the master node from <b>Master Node Group (Master AZ)</b>. </li><li>For multi-AZ deployment, select a master AZ from the drop-down list of <b>Master Node Group (Master AZ)</b> and specify an AZ for the replica from the drop-down list of replica x, where x is the replica number, such as replica 1 and replica 2.</li></ul></tr>
   <tr>
   <td>IPv4 Network</td>
       <td>Select a VPC and subnet. We recommend you select the same <a href="https://cloud.tencent.com/document/product/215">VPC</a> in the same region as the CVM instance to be connected to. After purchasing a TencentDB instance, you can switch its network from classic to VPC, but not vice versa. You can also click <b>Create VPCs</b> and <b>Create Subnets</b> to create a required network environment as instructed in <a href="https://intl.cloud.tencent.com/document/product/215/31805">Creating VPCs</a>.</td></tr>
   <tr>
   <td>Port</td>
   <td>Custom port. Value range: 1024–65535.</td></tr>
   <tr>
   <td>Parameter Template</td>
   <td>Apply a parameter template to configure parameters in batches for the instance. For more information, see <a href="https://intl.cloud.tencent.com/document/product/239/41810">Applying Parameter Templates</a>.</td></tr>
   <tr>
   <td>Project</td>
   <td>Assign your instance to a project for easy management.</td></tr>
   <tr>
   <td>Tag</td>
   <td>Add tags to your instance for easy classification and management. Click <b>Add</b> to select tag keys and values.</td></tr> 
   <tr>
   <td>Security Group</td>
   <td>Set security group rules to control the inbound/outbound traffic to/from your instance. You can either select a security group from the <b>Existing Security Groups</b> drop-down list or click <b>Custom Security Groups</b> to create one and set <b>inbound</b>/<b>outbound</b> rules. For more information, see <a href="https://intl.cloud.tencent.com/document/product/239/31945">Security Group</a>.</td></tr> 
   <tr>
   <td>Instance Name</td>
   <td>Enter up to 60 letters, digits, hyphens, and underscores.</td></tr>  
   <tr>
   <td>Set Password</td>
   <td><b>Password Authentication</b> is selected by default.</tr>   
   <tr>
   <td>Password</td>
   <td>Set an access password for the instance, which must meet the following requirements:<ul><li>It must contain 8–30 characters. </li><li>It must contain characters in at least two of the following character types: lowercase letters, uppercase letters, digits, and special symbols (()`~!@#$%^&*-+=_|{}[]:;<>,.?/). </li><li>It cannot start with a slash (/).</li></ul></td></tr> 
   <tr>
   <td>Confirm Password</td>
   <td>Enter the access password for the instance again.</td></tr>  
   <tr>
   <td>Quantity</td>
   <td>You can purchase up to 100 instances in each region and up to 30 instances each time.</td></tr> 
   </tbody></table>
3. After verifying that the parameters are correctly configured, click **Buy Now**. After the purchase success message is displayed, click **Go to Console** to enter the instance list page. After the instance's status becomes **Running**, you can use it.

>?
>- After activating TencentDB for Redis, make sure that your account balance is sufficient. An insufficient balance may cause overdue payments or even instance repossession. For more information, see [Payment Overdue](https://intl.cloud.tencent.com/document/product/239/31956).
>- For subsequent operations, see [Creating TencentDB for Redis Instance](https://intl.cloud.tencent.com/document/product/239/37712).


## Purchasing via API

| API                                                     | Description      |
| :----------------------------------------------------------- | :------------ |
| [CreateInstances](https://intl.cloud.tencent.com/document/product/239/32069) | Creates TencentDB for Redis instance |

