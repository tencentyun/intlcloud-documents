### What is the latest version of MongoDB?
Version 3.2.10 and 3.6.3 are available on TencentDB for MongoDB.
### How do I delete a MongoDB database? Will it be deleted automatically if I do not renew it after it expires?
An expired TencentDB for MongoDB instance will be automatically deleted if it is not renewed after the 14-day grace period. So please back up your data. You can go to **Operation** -> **More** -> **Return and Refund** in the instance list to terminate the instance manually through the console.
### How do I apply for security credentials for MongoDB?
Before using Tencent Cloud's APIs for the first time, you need to apply for security credentials on **Tencent Cloud Console** -> **[API Key Management](https://console.cloud.tencent.com/cam/capi)**. 
Security credentials consist of a SecretId and a SecretKey, where:
-  **SecretId**：Identify of the requester.
- **SecretKey**: a key that can be used to encrypt the strings to create a signature so that Tencent Cloud server can validate the identity of the requester.
>!!SecretKeys are very important through which you can access and work with the resources in your Tencent Cloud account via API. For security reasons, please keep your keys safe and rotate them regularly, and make sure you delete the old key after a new one is created. For more information, see [Signature Method](https://cloud.tencent.com/document/product/240/8329).
### What are the restrictions on creating MongoDB user names?
Tencent Cloud has two default user types: rwuser and mongouser. The role for the built-in users is [readWriteAnyDatabase+dbAdmin](https://docs.mongodb.com/v3.0/reference/built-in-roles/). That is, you can read and write, but not perform critical operations on any of the databases.
For certain versions of MongoDB, some instances support only rwuser (Tencent Cloud will upgrade these instances and we will contact you before the upgrade.).
You can manage your accounts and permissions on TencentDB for MongoDB Console to meet your business needs. For more information, see [Use Limits](https://cloud.tencent.com/document/product/240/622).
### What Nodes are supported for MongoDB?
Tencent Cloud managed data centers are distributed in different locations across the globe, covering South China, East China, and North China, Southeast Asia (covered by IDC in Hong Kong) and North America (covered by IDC in Toronto)
Tencent Cloud is deploying more Nodes globally to cover more Regions. A Node consists of Regions and Availability Zones.
- **Region**
Available Regions:
Mainland China: South China (Guangzhou), East China (Shanghai), North China (Beijing).
Outside Mainland China: Southeast Asia (Hong Kong) and North America (Toronto).
- **Node**
In a Region, Availability Zones refer to Tencent Cloud physical IDCs with independent power facilities and networks.
Availability Zones are designed to prevent single point failures (except for large-scale natural disasters or major power failures) from affecting other Availability Zones in the same region to ensure your business availability.
  [South China] Guangzhou Zone 1 (Stockout), Guangzhou Zone 2, Guangzhou Zone 3<br/>
  [East China] Shanghai Zone 1<br/>
  [North China] Beijing Zone 1<br/>
  [Southeast Asia] Hong Kong Zone 1<br/>
  [North America] Toronto Zone 1<br/>
For more information, see [Regions and Availability Zones](https://cloud.tencent.com/document/product/240).
