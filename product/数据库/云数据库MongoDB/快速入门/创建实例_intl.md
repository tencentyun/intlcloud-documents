Log in to the [Tencent Cloud official website](https://cloud.tencent.com/), click the menu as shown in the following figure and enter the [MongoDB Overview](https://cloud.tencent.com/product/mongodb) page.
![](https://main.qcloudimg.com/raw/0ca36011c0ea72c457079c869a3149d7.png)
Click **Buy Now** and enter the [product purchase page](https://buy.cloud.tencent.com/mongodb).
![](https://main.qcloudimg.com/raw/db8d147eeb15b9716516cf40271d4b04.png)

You can modify settings on the product purchase page as described below.

### Billing Options and Region ###
#### Billing Options ####
TencentDB for MongoDB is pay-as-you-go, making it very suitable for businesses with needs that can fluctuate instantaneously or unpredictable sales volume. This billing method is also recommended for users with temporary and sudden resource requirements. Pay-as-you-go is a postpay billing method. When you create a document database, we will freeze the hardware cost of one hour in your Tencent Cloud account and charge the usage fee on the dot of each hour (Beijing time). The billing time is accurate down to the second. With the pay-as-you-go billing method, you only need to pay for what you use, and no upfront payment is required.

#### Region ####
Tencent Cloud managed data centers are located globally, including 4 regions in China (South China, East China, North China, and Southwest China), and more than 6 regions across the globe (Southeast Asia, Asia Pacific, Western U.S., Eastern U.S., North America, Europe, etc.). We are deploying more nodes to achieve higher global coverage. Currently, the regions that support instance creation include Guangzhou, Shanghai, Beijing, Chengdu, Chongqing, Hong Kong, Singapore, Seoul, Mumbai, Bangkok, Silicon Valley, Toronto, Virginia, Frankfurt, and Moscow. Available finance zones include Shenzhen Finance and Shanghai Finance.

Notes: 
 - While cloud products deployed within the same region can communicate with each other over the private network, the private networks for the resources in different accounts are completely isolated from each other.
- Cloud products in different regions cannot communicate with each other over a private network.
- Because each region is independent, cross-region access to Tencent Cloud resources is not supported through private networks.
- When you purchase Tencent Cloud resources, we recommend you select a region closest to your customers to minimize connection latency.
#### Availability Zones ####
Availability Zones refer to Tencent Cloud physical IDCs with independent power facilities and networks within a same region. Availability Zones are designed to prevent single point failures (except for large-scale natural disasters or major power failures) from affecting other Availability Zones in the same region to ensure your business availability. Availability Zones in the same Region are connected via low-latency private networks.
### Basic Configurations ####
The basic configuration includes the configuration of server type, database version, storage engine, instance type, number of shard nodes, computing resource specification, and storage capacity. See below for details.
#### Configuration Types ####
Two types of models are available: High IO and High IO (10 GB).
#### Version ####
The version 3.2 and 3.6 are available.
#### Engine ####
TencentDB for MongoDB supports two storage engines: WiredTiger and Rocks.
#### Instance type and number of nodes ####
Instance types include replica set and sharded instances. For replica set instances, the "1 Master and 2 Slaves" architecture is configured by default. For sharded clusters, you can select the number of shards and the number of nodes in each shard as needed. Each shard has "1 Master and 2 Slaves" by default. To improve data availability, you can increase the number of nodes in each shard. To increase the storage capacity of the cluster, you can increase the number of shards.
#### Specification ####
The table below shows the available computation specifications for each node:
| CPU | MEM |
| 1 core | 2 GB |
| 2 cores | 4 GB |
| 4 cores | 8GB |
| 6 cores | 16GB |
| 12 cores | 32GB |
| 24 cores | 64GB |
| 24 cores | 128GB |
| 32 cores | 240GB |
#### Capacity ####
You can select storage specifications according to computation specifications. The storage space of Oplog is 10% of the configured storage capacity by default, you can adjust the percentage in Tencent Cloud Console.
### Network and Project ###
#### Network type ####
VPC networks and basic networks are supported. If you select a basic network, only devices in the basic network can access the database instances you created. If you select a VPC network, only devices in the current subnet can access the database instances you created.
#### Project ####
You can select a project based on your business needs.
### Purchase Quantity and Usage Period ###
#### Purchase quantity ####
Each user can purchase up to 30 pay-as-you-go instances in all regions.

