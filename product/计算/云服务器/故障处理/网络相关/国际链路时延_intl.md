## Problem Description
The latency is too long when users log in to CVMs located in North America.
Due to the small number of international routing egresses within the country and other factors, high concurrency may cause serious congestion of the international linkage and make the access unstable. Tencent Cloud has reported this issue to the ISP. If you need to manage and operate a CVM located in North America at home, in the short term, you can purchase a CVM located in Hong Kong (China) and use it as a transfer point to log in to the CVM located in North America.

<!--![](https://main.qcloudimg.com/raw/53a963a1e25048a0a05aa7d5b54ca943.png)-->

## Solution
 1. [Purchase](https://buy.cloud.tencent.com/cvm?tabIndex=1) a Windows CVM located in Hong Kong (China) as a jump server in the custom configuration page (Windows operating systems support login to both Windows and Linux CVMs located in North America).
	
	>**Note:**
>You need to buy at least 1 Mbps bandwidth, or you will be unable to log in to the jump server.

 2. After the purchase is made successfully, log in to the Windows CVM located in Hong Kong (China) :

[Log in to a Windows CVM with a public IP from a Windows machine](https://intl.cloud.tencent.com/document/product/213/5435)

[Log in to a Windows CVM from console VNC](https://intl.cloud.tencent.com/document/product/213/5435)

 3. Log in to your CVM located in North America from the Windows CVM located in Hong Kong (China) :

- Log in to a Linux CVM located in North America

[Log in to a Linux CVM with a public IP from a Windows machine using password](https://intl.cloud.tencent.com/document/product/213/5436)

- Log in to a Windows CVM located in North America 

[Log in to a Windows CVM with a public IP from a Windows machine](https://intl.cloud.tencent.com/document/product/213/5435)

[Log in to a Windows CVM from console VNC](https://intl.cloud.tencent.com/document/product/213/5435)

