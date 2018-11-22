Tencent Cloud currently offers a number of available regions: **East China (Shanghai), South China (Guangzhou), Hong Kong and North America**. In addition, financial institutions and enterprises can apply for activating services in the **Shanghai financial availability zone** by submitting tickets.
**Note:**
1. Cloud services in the same region can interconnect with one another through private network.

2. Cloud services in different regions cannot interconnect with one another through private network.
 - CVM supports cross-region interconnection through private network but does not support cross-region access to TencentDB or Cloud Memcached;
 - When binding a CVM instance for CLB, only the instances in the same region can be selected;
 - A CVM instance can access CVM and COS instances in another region through public network.
 
3. When purchasing a CVM instance, you are recommended to select the region closest to your end users, which can reduce the access latency and increase the download speed.

4. For users of pay-per-use CVM and TencentDB, pay-per-use resources can be purchased only in the Guangzhou region, and if resources in other regions are wanted for purchase, the pay-per-use billing method needs to be changed to prepaid first.

**Special Note for Hong Kong:**
1. Currently, the following cloud services are available in Hong Kong: CVM, CLB, TencentDB, CDN, etc.
(Note: TencentDB can only be purchased by users in the whitelist.)
2. The following cloud services are not available for the time being: Cloud Memcached, COS, Cloud Block Storage, One-Click Service or Partition Service Domain Binding.
3. If you need to log in to a CVM instance in the Hong Kong region, you are recommended to log in with a jump server for a better OPS experience.

**Special Note for North America:**
1. Currently, the following cloud services are available in North America: CVM, TencentDB, Cloud Memcached, CLB, VPC, CDN, Cloud Monitor, etc.
2. The following cloud services are not available for the time being: Cloud Block Storage, COS, Mobile CDN, Cloud Automated Testing, One-Click Service or Partition Service Domain Binding.
3. Due to the high latency between the North America and China, if you need to log in to a CVM instance in the North America region, you are recommended to log in with a jump server for a better OPS experience.
Note: The interconnection through private network above refers to the interconnection of resources under the same account, while the resources under different accounts are completely isolated.

**Special Note for Shanghai Financial Availability Zone:**
This is a tailor-made availability zone for compliance with regulatory requirements in the finance industry and features high security and high isolation. Currently, it provides services such as CVM, finance database, Redis storage and face recognition, which can be applied for by verified financial customers by submitting tickets.
