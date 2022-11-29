## Overview

This document describes how to configure a routing rule in the CKafka console to enhance network access control in public/private network transfers. For more information on public network access, see [Configuring ACL Policy](https://intl.cloud.tencent.com/document/product/597/39084).

| Route Type | VPC | Public Domain Name Access |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Access mode | <li>PLAINTEXT</li><li>SASL_PLAINTEXT</li><li>SASL_SSL (only supported by Pro Edition instances)</li><li>SASL_SCRAM (only supported by instances on v2.4.1; for existing instances, you need to <a href = "https://console.intl.cloud.tencent.com/workorder/category">submit a ticket</a> for application)</li> | <li>SASL_PLAINTEXT</li><li>SASL_SSL (only supported by Pro Edition instances)</li> |



## Directions

> ?Up to 5 routes can be created per instance. There is only one route if the SASL_PLAINTEXT access mode is selected. For example, if the SASL_PLAINTEXT access mode is selected for the route type of public domain access, the SASL_PLAINTEXT access mode cannot be selected when other routes are created.

<dx-tabs>

::: VPC

**Operation scenario**: When purchasing an instance, if you select VPC and choose a corresponding VPC environment (such as VPC A), then CKafka services (such as data production and consumption) can be accessed only from VPC A. If you subsequently find that you need to access the CKafka services in VPC A from other VPCs (such as VPC B), you can select an appropriate routing policy for VPC by configuring the access mode.<br>

**Suggestion**: To ensure security, this access mode provides user management and ACL policy configuration to manage user access permission. Configure as appropriate.<br>

**Directions:**

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. On the instance's basic information page, click **Add a routing policy** in the **Access Mode** module.
4. In the pop-up window, select **VPC Network** as the route type and select the access mode and network.
   ![](https://main.qcloudimg.com/raw/e3c2304070064b93e082895b9bd7b9b2.png)
   <dx-alert infotype="explain" title="">
   If you select VPC access, you can specify the IP to keep it unchanged when changing the access mode.
   </dx-alert>
5. Click **Submit** to add the VPC network.
6. Click **View All IPs and Ports** in the **Operation** column to view the list of IPs and ports that should be opened.

>? As broker scaling and migration will cause port changes, do not add only the current listed ports; otherwise, message read/write may become abnormal after scaling and migration. If your server is configured with access restrictions (security groups), you should open the following port ranges on the server:
>- Port range that should be opened for the VPC route: 9092–60000
>- Port range that should be opened for the public network route: 50000–53000
>- Port range that should be opened for the supportive route: 6000–12000

![](https://qcloudimg.tencent-cloud.cn/raw/50155761eff6298b4598aa674161e05c.png)

::: 

::: Public domain name access
**Operation scenario**: If your consumer or producer is located in a self-built data center or another cloud, you can produce and consume data in CKafka through public network access.<br>

**Suggestion**: To ensure security, Kafka offers various security authentication mechanisms, which mainly fall into the SSL and SASL2 categories. Among them, SASL/PLAIN is an authentication method based on account and password and more commonly used. CKafka supports SASL_PLAINTEXT and SASL_SSL authentication. We recommend you configure the authentication method as appropriate when selecting public domain name access.<br>

**Directions:**

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. On the instance's basic information page, click **Add a routing policy** in the **Access Mode** module.
4. In the pop-up window, select **Public domain name access** as the route type and select the access mode and network.
    ![](https://main.qcloudimg.com/raw/c4d1852255a63b38bfc199d3b6d1711b.png)
5. Click **Submit** to add the public network routing policy.
6. Click **View All IPs and Ports** in the **Operation** column to view the list of IPs and ports that should be opened.
    <dx-alert infotype="explain" title="">
  - As broker scaling and migration will cause port changes, do not add only the current listed ports; otherwise, message read/write may become abnormal after scaling and migration. If your server is configured with access restrictions (security groups), you should open the following port ranges on the server:
    - Port range that should be opened for the VPC route: 9092–60000
    - Port range that should be opened for the public network route: 50000–53000
    - Port range that should be opened for the supportive route: 6000–12000
  - CKafka provides 3 Mbps public network bandwidth free of charge by default, which can be increased for Pro Edition instances. For detailed directions, see [Public Network Bandwidth Management](https://intl.cloud.tencent.com/document/product/597/42386).
    </dx-alert>
    ![](https://qcloudimg.tencent-cloud.cn/raw/50155761eff6298b4598aa674161e05c.png)
    
    :::
    </dx-tabs>
