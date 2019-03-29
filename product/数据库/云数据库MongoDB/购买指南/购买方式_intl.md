Log in to the [Tencent Cloud official website](https://cloud.tencent.com/), select MongoDB from the product menu (as shown below) and go to the [MongoDB Overview](https://cloud.tencent.com/product/mongodb) page.
![](https://main.qcloudimg.com/raw/0ca36011c0ea72c457079c869a3149d7.png)
Click **Get Started** to go to the [product purchase page](https://buy.cloud.tencent.com/mongodb).
![](https://main.qcloudimg.com/raw/db8d147eeb15b9716516cf40271d4b04.png)
The product purchase page mainly covers the following settings, which are described in detail below.
### Billing method and region ###
#### Billing method ####
The monthly subscription and pay as you go billing methods are supported. Pay as you go is applicable to scenarios where the business volume fluctuates dramatically at a certain time. This billing method is recommended for scenarios with high and unpredictable fluctuations in business development or temporary and sudden requirements for resources. When you create a document database, the hardware cost of one hour is frozen in your Tencent Cloud account and charged at each o'clock (Beijing time), with the billable time accurate down to the second. With the pay-as-you-go billing method, you only need to pay for the actual usage of TencentDB for MongoDB with no upfront payment required. Monthly subscription is applicable to long-cycle businesses with stable volume, and is more economical than the pay as you go method. Monthly subscription is a prepaid billing method. In this method, you prepay the fee for TencentDB for MongoDB for a single month or multiple months/years based on your business needs.
#### Region ####
Tencent Cloud's hosting data centers are distributed globally, covering South China, East China, North China, and Southwest China, as well as Southeast Asia, Asia Pacific, Western U.S., Eastern U.S., North America, Europe, etc. We will gradually increase available nodes to cover more regions. Supported regions are Guangzhou, Shanghai, Beijing, Chengdu, Chongqing, Hong Kong, Singapore, Seoul, Mumbai, Bangkok, Silicon Valley, Toronto, Virginia, Frankfurt, and Moscow. Supported finance zones include Shenzhen Finance and Shanghai Finance.<br>
Notes: <br>
- Cloud products in the same region communicate with each other over a private network, but the private networks for the resources under different accounts are completely isolated from each other.
- Cloud products in different regions cannot communicate with each other over a private network.
- Tencent Cloud resources in different regions cannot access each other over a private network.
- It is recommended that you select a region closest to your customers when purchasing cloud services, so as to minimize the access latency.

#### Availability zone #### 
Availability zones are Tencent Cloud's physical IDCs with power facilities and networks independent of each other within the same region. They are designed to ensure that failures within an availability zone can be isolated (except for large-scale disaster or major power failure) without spreading to other zones, so as to ensure your business stability. Availability zones in the same region communicate with each other over a private network, and network latency is shorter for products within the same availability zone.
### Basic configuration ####
The basic configuration mainly involves server type, database version, storage engine, instance type, number of shard nodes, computing resource specification, storage capacity, etc. See below for details.
#### Configuration type ####
Two types of models are available: High IO and High IO (10 GB).
#### Version ####
The version 3.2 is available and version 3.6 will be released soon.
#### Engine ####
TencentDB for MongoDB supports two storage engines: WiredTiger and Rocks.
#### Instance type and number of nodes ####
Instance types include replica set and sharding instances. If replica set instances are used, the "1 Master, 2 Slaves" architecture is configured by default. When a sharding cluster is used, you can select the number of shards and the number of nodes in each shard as needed. The "1 Master, 2 Slaves" architecture is used in each shard by default. To improve data availability, you can increase the number of nodes in each shard. To expand the storage capacity of the cluster, you can increase the number of shards.
#### Specification ####
Computation specifications supported for each node are shown in the following table:<br>

| CPU | MEM | 
| ------- |-------|
| 1 core | 2 GB |
| 2 cores | 4 GB |
| 4 cores | 8GB |
| 6 cores | 16GB |
| 12 cores | 32GB |
| 24 cores | 64GB |
| 24 cores | 128GB |
| 32 cores | 240GB |

#### Capacity ####
You can select storage specifications according to computation specifications. The storage space of Oplog is 10% of the selected storage capacity by default, which can be adjusted on the Tencent Cloud Console.
### Network and project ###
#### Network type ####
VPCs and basic networks are supported. If you select a basic network, only devices in the basic network can access the created database instances. If you select a VPC, only devices in the current subnet can access the created database instances.
#### Project ####
You can select appropriate projects based on your business needs.
### Purchase quantity and usage period ###
#### Purchase quantity ####
You can purchase a maximum of 10 monthly subscription instances, and a maximum of 30 pay-as-you-go instances in all regions.
#### Usage period ####
In the monthly subscription billing mode, you can select a usage period of 3 years at most. You can also enjoy 12% off for a usage period of more than 6 months, 60% off for a usage period of 2 years and 70% off for a usage period of 3 years.

