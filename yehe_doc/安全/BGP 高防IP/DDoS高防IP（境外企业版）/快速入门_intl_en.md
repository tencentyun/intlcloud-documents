Anti-DDoS Advanced (Global Enterprise Edition) is a paid service aimed at global users with businesses deployed in Tencent Cloud to improve their global DDoS protection capabilities.
- It allows you to purchase and hold public IP address resources independently.
- After it is bound to cloud resources, the cloud resources can communicate with the public network through it.

This document takes binding an Anti-DDoS Advanced (Global Enterprise Edition) instance and a cloud resource as an example to describe the usage lifecycle of Anti-DDoS Advanced (Global Enterprise Edition).

## Background
The usage lifecycle of Anti-DDoS Advanced (Global Enterprise Edition) includes purchasing Anti-DDoS Advanced (Global Enterprise Edition) instance, configuring protection rules for the instance, configuring application rules for the instance, and terminating the instance.
![](https://main.qcloudimg.com/raw/95b31a570ba0a1d479db4e65f58ef070.png)

1. [Purchasing Anti-DDoS Advanced (Global Enterprise Edition) instance](https://buy.cloud.tencent.com/antiddos#/advanced-intl): purchase Anti-DDoS Advanced (Global Enterprise Edition) resources according to your actual needs.
2. [Configuring protection rules](https://intl.cloud.tencent.com/document/product/297/34092) for the Anti-DDoS Advanced (Global Enterprise Edition) instance: configure protection policies that fit your application.
3. Configuring application rules for the Anti-DDoS Advanced (Global Enterprise Edition) instance: associate the instance with the cloud resources to be protected.
4. Terminating Anti-DDoS Advanced (Global Enterprise Edition) instance: after unassociating the instance from cloud resources, you can associate the instance with other cloud resources. The unassociating operation may cause the network of the corresponding cloud resource to be disconnected, and instances that are not bound to cloud resources will incur IP resource fees.

## Operation Directions
### Purchasing Anti-DDoS Advanced (Global Enterprise Edition) instance
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition)](https://console.cloud.tencent.com/ddos/ddos-basic) console.
2. Refer to the [Purchase Directions](https://intl.cloud.tencent.com/zh/document/product/297/37241) to purchase an instance.
3. Click **Anti-DDoS Advanced (New)** -> **Service Packages** in the left sidebar to view the purchased Anti-DDoS Advanced (Global Enterprise Edition) instance, which is not bound.
>?We recommend binding cloud resources to the Anti-DDoS Advanced (Global Enterprise Edition) instance promptly so as to save IP resource fees. IP resource fees are charged by hour accurate to the second level, and if the duration is less than one hour, fees will be charged according to the proportion of idle time. Therefore, please bind cloud resources in time. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/zh/document/product/297/37240).
>
 ![](https://main.qcloudimg.com/raw/af5473e5d77eb2482da378f811024f44.jpg) 

### Configuring protection rule
Log in to the [Anti-DDoS Advanced (Global Enterprise Edition)](https://console.cloud.tencent.com/ddos/ddos-basic) console, click **Anti-DDoS Advanced (New)** -> **Service Packages** in the left sidebar, select the corresponding instance, and click **Protection Configuration**. For more information on the configuration methods, please see [Configuring Cleansing Threshold and Protection Level](https://intl.cloud.tencent.com/document/product/297/34092).
![](https://main.qcloudimg.com/raw/66d63a0ddf596cf30309d4f3b1c83af8.png) 
### Associating cloud resource
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition)](https://console.cloud.tencent.com/ddos/ddos-basic) console and click **Anti-DDoS Advanced (New)** -> **Application Accessing** in the left sidebar.
2. Select **IP Access**, click **Add Rule**, and then the resource binding window will pop up.
3. Select the Anti-DDoS Advanced (Global Enterprise Edition) instance and the CVM instances that need to be protected, click **OK**.
![](https://main.qcloudimg.com/raw/b2a2c76d648453401f3a32c45e5b5196.png)

### Unassociating cloud resource
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition)](https://console.cloud.tencent.com/ddos/ddos-basic) console and click **Anti-DDoS Advanced (New)** -> **Application Accessing** in the left sidebar.
2. Select **IP Access** and click **Delete** to unassociate.
![](https://main.qcloudimg.com/raw/9c366082b1b9a21f4ff1192a748d8872.jpg)
