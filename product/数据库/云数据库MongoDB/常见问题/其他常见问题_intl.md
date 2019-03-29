### What is the latest version of MongoDB?
TencentDB for MongoDB 3.2.10 and 3.6.3 are available.

### How do I delete a MongoDB database? Will it be deleted automatically if I do not review it after it expires?
A TencentDB for MongoDB instance is automatically terminated if it is not renewed upon expiration. So please confirm and back up your data. You can go to **Operation** -> **More** -> **Return and Refund** in the instance list on the console to terminate the instance manually.

### How do I apply for security credentials for MongoDB?
Before calling a Cloud API for the first time, you need to apply for security credentials on the Tencent Cloud CVM Console.
Security credentials consist of a SecretId and a SecretKey, where:
 - SecretId is used to identify the API caller.
 - SecretKey is a key used for signature string encryption, and signature string verification by the server.

>!API key is very important for building Tencent Cloud API requests. With Tencent Cloud APIs, you can work with all of your Tencent Cloud resources under your account. For the security of your property and services, keep the key well and change it regularly (after changing the key, be sure to delete the old one as soon as possible). For more information, see [Signature Method](https://cloud.tencent.com/document/product/240/8329).
 
### What are the restrictions when using the MongoDB user name?
Tencent Cloud comes with two default users: rwuser and mongouser. The role for the built-in users is [readWriteAnyDatabase+dbAdmin](https://docs.mongodb.com/v3.0/reference/built-in-roles/), that is, you can read and write any database, but are not permitted to perform critical operations.
Depending on the version of MongoDB, some instances only have rwuser (Tencent Cloud will upgrade such instances and we will contact you before doing so).
You can manage your accounts and permissions on the Console of TencentDB for MongoDB to meet your business needs. For more information, see [Use Limits](https://cloud.tencent.com/document/product/240/622).
 
### What nodes are supported for MongoDB?
Tencent Cloud hosting data centers are distributed in different locations across the globe. In Mainland China, they cover South China, East China and North China. The Hong Kong node covers Southeast Asia and the IDC node in Toronto covers North America.
Tencent Cloud will gradually increase available nodes to cover more regions. All nodes consist of regions and availability zones.
 - **Region**
The following available regions are offered by Tencent Cloud:
Mainland China: South China (Guangzhou), East China (Shanghai), North China (Beijing).
Outside Mainland China: Southeast Asia (Hong Kong) and North America (Toronto).
 - **Node**
Availability zones are Tencent Cloud's physical IDCs with power facilities and networks independent of each other within the same region.
They are designed to ensure that failures within an availability zone can be isolated (except for large-scale disaster or major power failure) without spreading to other zones, so as to ensure your business stability.
[South China] Guangzhou Zone 1 (Stockout), Guangzhou Zone 2, Guangzhou Zone 3
[East China] Shanghai Zone 1
[North China] Beijing Zone 1
[Southeast Asia] Hong Kong Zone 1
[North America] Toronto Zone 1
For more information, see [Regions and Availability Zones](https://cloud.tencent.com/document/product/240/3637).
 


