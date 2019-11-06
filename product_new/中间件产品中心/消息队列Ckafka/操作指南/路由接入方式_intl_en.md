## Operation Scenarios
This task guides you through how to configure a routing rule in the CKafka Console to enhance network access control in public/private network transfer. For more information on public network access.<!-- see [User Access Control (ACL and User Management)]()-->

## Prerequisites
This feature is currently under beta test. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=335&source=0&data_title=%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97CMQ/CKAFKA/IoT%20MQ&step=1) for application.
>? Up to 5 routes can be created for an instance. There is only one route if the SASL_PLAINTEXT access mode is selected. For example, if SASL_PLAINTEXT is selected for the route type of public domain name access, you cannot select SASL_PLAINTEXT again when creating other routes.

## Directions
1. On the instance basic information page, click **Add a routing policy** in the "Access Mode" module.
2. Select the route type and access mode in the popup window.
Route Type: VPC or public domain name access, as described below:
 - **VPC**
Operation scenario: When purchasing an instance, if you select VPC and choose a corresponding VPC environment (such as VPC A), then CKafka services (such as data production and consumption) can be accessed only from VPC A. If you subsequently find that you need to access the CKafka services in VPC A from other VPCs (such as VPC B), you can select an appropriate routing policy for VPC by configuring the access mode.
Suggestions: To ensure security, this access mode supports user management and ACL policy configuration to manage user access permission. Please configure as appropriate.
![](https://main.qcloudimg.com/raw/f91dd0f14b5728f0af914de187bfcc6d.png)
>?The VPC access address provided in the console (such as `172.16.0.12:9092`) represents the communication address used to obtain the backend service. There may be multiple ports in a real access address. Please open all ports after 9092 to the internet on your server, so that the service can be accessed normally.
 - **Public domain name access**
Operation scenario: If your consumer or producer is located in a self-built data center or another cloud, you can produce and consume data in CKafka through public network access.
Suggestions: To ensure security, Kafka offers various security authentication mechanisms, which mainly fall into the SSL and SASL2 categories. Among them, SASL/PLAIN is an authentication method based on account and password and more commonly used. CKafka supports SASL_PLAINTEXT authentication. You are recommended to configure the authentication method as appropriate when selecting public domain name access.
![](https://main.qcloudimg.com/raw/c68d11b05638632b2f0f862feb0881eb.png)
3. Click **Submit** to add the routing policy.
