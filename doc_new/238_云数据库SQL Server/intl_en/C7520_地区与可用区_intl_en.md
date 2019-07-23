TencentDB for SQL Server is available in multiple regions, including East China (Shanghai), South China (Guangzhou), North China (Beijing), Finance Zone (Shanghai and Shenzhen), Southeast Asia (Hong Kong), and Korea (Seoul).
- The edition of SQL Server available in East China (Shanghai), South China (Guangzhou), North China (Beijing), Finance Zone (Shanghai and Shenzhen), and Southeast Asia (Hong Kong) is Enterprise, while that in Korea (Seoul) is Standard.
- Currently, Finance Zone (Shanghai and Shenzhen) and Southeast Asia (Hong Kong) only support monthly subscription (prepaid), while Korea (Seoul) only supports pay-as-you-go billing (postpaid).

>?
- Tencent Cloud services in the same region can communicate with one another over private networks.
- Tencent Cloud services in different regions cannot communicate with one another over private networks.
   - CVM supports cross-region communication over private networks but does not support cross-region access to TencentDB or Cloud Memcached.
   - When a CVM is bound for CLB, only the CVMs in the same region can be selected.
   - A CVM instance can access CVM and COS instances in another region over public networks.
- When purchasing Tencent Cloud services, you are recommended to select the region closest to your end users so as to minimize access latency and improve download speed.
- Tencent Cloud provides pay-as-you-go CVM and TencentDB resources only in Guangzhou. If you want to purchase them in other regions such as Shanghai, you need to change the purchase mode to "Prepaid".

**Special note for Hong Kong:**
- Currently, the following cloud services are available in Hong Kong: CVM, CLB, TencentDB, CDN, GAAP, Cloud Monitor, CAT, Cloud Security, Mobile Security, key factor, and Fusion SDK.
>! TencentDB can only be purchased by users in the whitelist.
- The following Tencent Cloud services are not available for the time being: Cloud Memcached, COS, CBS, One-Click Service, and Region-specific Server Domain Name Binding.
- When you need to log in to a CVM instance in Hong Kong, login via a jump server is recommended for a better OPS experience.

**Special note for Finance Zone:**
Finance Zone is an availability zone customized for financial industry regulatory compliance. It has high security and high isolation, and it currently provides services such as CVM, finance database, Redis storage and face recognition. Verified customers in the finance industry can apply for a finance zone by [submitting a ticket](https://console.cloud.tencent.com/workorder/category). For more information, see [Finance Zone Overview](http://cloud.tencent.com/doc/product/304/%E9%87%91%E8%9E%8D%E4%BA%91%E7%AE%80%E4%BB%8B).
