TencentDB for SQL Server is available in multiple regions, including East China (Shanghai), South China (Guangzhou), North China (Beijing), China (Hong Kong) , and Korea (Seoul).
- The SQL Server Enterprise edition is available in East China (Shanghai), South China (Guangzhou), North China (Beijing) and China (Hong Kong) . The Standard edition is available in Korea (Seoul).
- Korea (Seoul) only supports pay-as-you-go billing.

>?
- Tencent Cloud services in the same region can communicate with one another over private networks.
- Tencent Cloud services in different regions cannot communicate with one another over private networks.
   - CVM supports cross-region communication over private networks but does not support cross-region access to TencentDB or Cloud Memcached.
   - When a CVM is bound for CLB, only the CVMs in the same region can be selected.
   - A CVM instance can access CVM and COS instances in another region over public networks.
- When purchasing Tencent Cloud services, you are recommended to select the region closest to your end users so as to minimize access latency and improve download speed.
- Tencent Cloud provides pay-as-you-go CVM and TencentDB resources only in Guangzhou. If you want to purchase them in other regions such as Shanghai, you need to change the purchase mode to "Prepaid".

**Special note for Hong Kong, China:**
- Currently, the following cloud services are available in Hong Kong: CVM, CLB, TencentDB, CDN, GAAP, Cloud Monitor, CAT, Cloud Security, Mobile Security, key factor, and Fusion SDK.
>! TencentDB can only be purchased by users in the whitelist.
- The following Tencent Cloud services are not available for the time being: Cloud Memcached, COS, CBS, One-Click Service, and Region-specific Server Domain Name Binding.
- When you need to log in to a CVM instance in Hong Kong, login via a jump server is recommended for a better OPS experience.

