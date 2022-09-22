## Overview
Based on Tencent Security's massive amounts of threat data, Tencent Cloud Workload Protection Platform（CWPP) leverages machine learning to provide a wide variety of security services ranging from intrusion detection to vulnerability alerting. It offers various security features such as brute force attack prevention, unusual login location reminding, trojan protection, and high-risk vulnerability detection, helping build a security protection system to cope with major network security risks faced by servers and prevent data leakage.

CWPP is available in Basic and Pro editions. When creating a CVM instance, you can choose to activate CWPP Basic by default.


<dx-alert infotype="explain" title="">
For more information on the features of CWPP Basic and Pro editions and their differences, see [Features in Different Editions](https://intl.cloud.tencent.com/document/product/296/2222).
</dx-alert>



## Billing Mode
CCWPP Basic is free of charge. 


## Installing CWPP Basic
You can install CWPP Basic in one of the following methods based on the actual conditions:
<dx-tabs>
::: Automatic installation during CVM instance creation
When creating a CVM instance, you can choose to activate CWPP Basic by default. On the CVM instance purchase page, select **Enable for Free** for **Security Reinforcement** to automatically install CWPP as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/0fdf0fddce3b59f80bdd337c1cf74e86.png)
:::
::: Manual installation for existing CVM instance
You can use one of the following methods to install CWPP for an existing instance based on its operating system:
- [Windows CVM environment](https://intl.cloud.tencent.com/document/product/296/12236)
- [Linux CVM environment](https://intl.cloud.tencent.com/document/product/296/12236)
:::
</dx-tabs>

After successful installation, you can view the security status of the CVM instance on the [overview page in the CVM console](https://console.cloud.tencent.com/cvm/overview) or in the [CWPP console](https://console.cloud.tencent.com/CWPP).


## See Also
- [Features in Different Editions](https://intl.cloud.tencent.com/document/product/296/2222)
- [Security Overview](https://intl.cloud.tencent.com/document/product/296/35234)
