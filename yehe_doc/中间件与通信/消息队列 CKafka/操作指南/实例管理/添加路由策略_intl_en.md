## Overview

This document describes how to configure a routing rule in the CKafka console to enhance network access control in public/private network transfers. For more information on public network access, please see [Configuring ACL Policy](https://intl.cloud.tencent.com/document/product/597/39084).

>?
>- CKafka supports SASL_SSL and SASL_PLAINTEXT authentication modes. The former is supported only for Pro Edition instances, and to use it, you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application (specific delivery process: you submit a ticket for application > a certificate is delivered to the broker server > a certificate is provided for client consumption).
>- Up to 5 routes can be created per instance. There is only one route if the SASL_PLAINTEXT access mode is selected. For example, if the SASL_PLAINTEXT access mode is selected for the route type of public domain name access, the SASL_PLAINTEXT access mode cannot be selected when other routes are created.

## Directions

<dx-tabs>

::: VPC

**Operation scenario**: when purchasing an instance, if you select VPC and choose a corresponding VPC environment (such as VPC A), then CKafka services (such as data production and consumption) can be accessed only from VPC A. If you subsequently find that you need to access the CKafka services in VPC A from other VPCs (such as VPC B), you can select an appropriate routing policy for VPC by configuring the access mode.


**Suggestion**: to ensure security, this access mode provides user management and ACL policy configuration to manage user access permission. Please configure as appropriate.

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. On the instance basic information page, click **Add a routing policy** in the **Access Mode** module.
4. In the pop-up window, select **VPC Network** as the route type and select the access mode and network.
![](https://main.qcloudimg.com/raw/e3c2304070064b93e082895b9bd7b9b2.png)
5. Click **Submit** to add the VPC network.

The VPC access address provided in the console (such as `172.16.0.12:9092`) represents the communication address used to obtain the backend service. There may be multiple ports in a real access address. Please open all ports after 9092 to the internet on your server, so that the service can be accessed normally.

::: 

::: Public\sdomain\sname\saccess
**Operation scenario**: if your consumer or producer is located in a self-built data center or another cloud, you can produce and consume data in CKafka through public network access.

**Suggestion**: to ensure security, Kafka offers various security authentication mechanisms, which mainly fall into the SSL and SASL2 categories. Among them, SASL/PLAIN is an authentication method based on account and password and more commonly used. CKafka supports SASL_PLAINTEXT authentication. You are recommended to configure the authentication method as appropriate when selecting public domain name access.

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. On the instance basic information page, click **Add a routing policy** in the **Access Mode** module.
4. In the pop-up window, select **Public domain name access** as the route type and select the access mode and network.
![](https://main.qcloudimg.com/raw/c4d1852255a63b38bfc199d3b6d1711b.png)
5. Click **Submit** to add the public network routing policy.
<dx-alert infotype="explain">
<ul>
 <li>CKafka provides 3 Mbps public network bandwidth free of charge by default, which can be increased to up to 198 Mbps for Pro Edition instances. For detailed directions, please see [Upgrading public network bandwidth](https://intl.cloud.tencent.com/document/product/597/42386).</li>
</ul>
</dx-alert>

:::
</dx-tabs>

