## Overview
Lighthouse uses the [Virtual Private Cloud](https://intl.cloud.tencent.com/document/product/215/535) automatically assigned by Tencent Cloud for network isolation. By default, Lighthouse instances cannot interconnect with other Tencent Cloud resources in VPCs such as CVM and TencentDB over the private network, and their interconnection needs to be implemented by associating a CCN instance. The interconnection feature is applicable to the following businesses:
 - Lighthouse access to CVM.
 - Lighthouse access to TencentDB.

<dx-alert infotype="explain" title="">
- Lighthouse instances in the same region under the same account are interconnected over the private network by default. For more information, see [Region and Interconnection](https://intl.cloud.tencent.com/document/product/1103/41266).
- Lighthouse and COS in the same region are interconnected over the private network by default with no need to be interconnected over CCN.
- Other Tencent Cloud resources need to use VPC to interconnect with Lighthouse.
</dx-alert>

This document describes how to associate/disassociate an instance with/from CCN in the Lighthouse console. For more information on CCN, see [Overview](https://intl.cloud.tencent.com/document/product/1003/30049).

## Must-knows
- The interconnection feature of Lighthouse is free of charge. You only need to pay attention to CCN billing information. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1003/30053). 
- CCN cross-MLC-border connections are not available for Lighthouse instances.
- Under the same account:
  - All Lighthouse instances in the same region are in the same VPC. A VPC can be associated with only one CCN instance.
  - Lighthouse instances in different regions are in different VPCs, which need to be associated with CCN instances separately.
- If there are no Lighthouse instances in a region, you cannot associate a CCN instance in that region.

## Directions

### Applying for Associating with a CCN[](id:association)
1. Log in to the Lighthouse console and select <b>[Interconnection](https://console.cloud.tencent.com/lighthouse/ccn/index)</b> on the left sidebar.
2. Select **Associate CCN Instance** in the target region.
![](https://qcloudimg.tencent-cloud.cn/raw/fdf2d7e60a095e95303e226c693cbfa2.png)
3. In the **Associate with CCN** pop-up window, select the target CCN instance and click **OK** to submit the association application.
![](https://qcloudimg.tencent-cloud.cn/raw/571bde6932f71d65a4bdb079a5d8e99a.png)
<dx-alert infotype="notice" title="">
1. If no CCN instances are available, create one as instructed in [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062).
- Only CCN instances under the same account can be associated with.
- After submitting the association application, log in to the [CCN console](https://console.cloud.tencent.com/vpc/ccn) in seven days to approve the application; otherwise, the application will expire, and you need to apply for association again.
</dx-alert>
4. Log in to the [CCN console](https://console.cloud.tencent.com/vpc/ccn), and click the ID/Name of the target CCN instance to open its details page.
![](https://qcloudimg.tencent-cloud.cn/raw/0c5badf89c0cf415a71cd4a51646685f.png)
5. On the CCN instance details page, select **Approve** on the right of the target association application.
Remarks "Lighthouse VPC" will be added to the VPC instance of Lighthouse by default. Select the correct instance as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/363bd10b3f88e60e86da7e3e58c2e6f8.png)
6. In the pop-up window, click **OK** to complete association. On the interconnection page, the region status will become **Connected**.
![](https://qcloudimg.tencent-cloud.cn/raw/019917af255fdbf6e0c1a86e28bfa4b4.png)
7. After the association is complete, check that the route is valid by following these steps:
  i. On the **Interconnection** page, click **CCN ID** under the region to go to the CCN details page.
  ii. On the CCN details page, select **Route Table** tab.
  iii. Confirm that the new routes are "valid". If there is a CIDR block conflict, the route may be invalid.
<dx-alert infotype="explain" title="">
To use invalid routes, see [Disabling Route](https://intl.cloud.tencent.com/document/product/1003/30068) and [Enabling route](https://intl.cloud.tencent. com/document/product/1003/30069). For conflict rules and restrictions, see [Use Limits](https://intl.cloud.tencent.com/document/product/1003/30052).
</dx-alert>
8. After associating the Lighthouse instance with CCN, 
you can associate Tencent Cloud resources such as CVM and TencentDB instances to CCN to implement interconnection. For more information, see [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).



### Disassociating from a CCN[](id:disassociate)
You can disassociate a CCN instance when the CCN association application status is **Applying**, **Expired**, or **Connected**. If the status is **Connected**, disassociation will interrupt the connections of all instances in the current region to other VPCs in CCN. Perform the following operations after confirming that they will not affect your business:
1. Log in to the Lighthouse console and select <b>[Interconnection](https://console.cloud.tencent.com/lighthouse/ccn/index)</b> on the left sidebar. 
2. Select **Disassociate** in the target region.
![](https://qcloudimg.tencent-cloud.cn/raw/565a447f7c1b5b9a147cb7706c1c634e.png)
3. In the **Disassociate from CCN** pop-up window, click **OK**.


## Examples of Interconnection Between Lighthouse with Cloud Resources
<dx-accordion>
::: Example 1: Interconnection Between Lighthouse and CVM

#### Scenario
The Lighthouse and CVM instances in the Guangzhou region are not interconnected by default and need to be associated with CCN for interconnection.

#### Steps
 1. Log in to the Lighthouse instance and run the following command:
```shellsession
ping CVM instance's private IP
```
If the following information is returned, the IP cannot be pinged:
![](https://main.qcloudimg.com/raw/49e76f62b5f7ae7e6fb504bf92b842a7.png)
 2. Associate with a CCN as instructed in [Applying for associating with a CCN](#association).
 Associate the VPC of CVM with the CCN instance as instructed in [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064). 
 3. Log in to the Lighthouse instance and run the following command:
```shellsession
ping CVM instance's private IP
```
If the following information is returned, the IP can be pinged and the interconnection succeeds.
![](https://main.qcloudimg.com/raw/b487ec4b7ae4be87059bd13db2f5f9b4.png)
:::
::: Example 2: Interconnection Between Lighthouse and TencentDB for MySQL

#### Scenario
In Guangzhou region, the Lighthouse and TencentDB for MySQL instructed in [Overview](https://intl.cloud.tencent.com/document/product/236/5147) are not interconnected by default. You need to associate MySQL with CCN to implement the interconnection.

#### Prerequisites
TencentDB for MySQL uses private network port `3306` by default. Allow this port in the inbound rules of the security group associated with the MySQL instance. For details, see [TencentDB Security Group Management](https://intl.cloud.tencent.com/document/product/236/14470).


#### Steps
1. Log in to the Lighthouse instance and run the following command to install `telnet`:
```shellsession
sudo yum install telnet -y
```
2. Run the following command to test whether the interconnection is successful or not.
```shellsession
telnet TencentDB for MySQL instance's private IP 3306
``` If the following information is returned, the interconnection fails.
![](https://main.qcloudimg.com/raw/e4faffa0bf9bb3448296d3bcae1c6dec.png)
3. Associate with a CCN as instructed in [Applying for associating with a CCN](#association).
 Associate the VPC of TencentDB for MySQL with the CCN instance as instructed in [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064). 
4. Log in to the Lighthouse instance and run the following command:
```shellsession
telnet TencentDB for MySQL instance's private IP 3306
``` If the following information is returned, the interconnection succeeds.
![](https://main.qcloudimg.com/raw/98f0b235240869f954b7dcfa23df202c.png)
5. Connect the Lighthouse instance to a MySQL instance as instructed in [Connecting to MySQL Instance](https://intl.cloud.tencent.com/document/product/236/37788).

:::
::: Example 3: Interconnection Between Lighthouse and TencentDB for Redis

#### Scenario
In Guangzhou region, the Lighthouse and TencentDB for Redis instructed in [Overview](https://intl.cloud.tencent.com/document/product/239/3205) are not interconnected by default. You need to associate Redis with CCN to implement the interconnection.

#### Prerequisites
TencentDB for Redis uses private network port `6397` by default. Allow this port in the inbound rules of the security group associated with the Redis instance. For details, see [Configuring Security Group](https://intl.cloud.tencent.com/document/product/239/31945).

#### Steps
1. Log in to the Lighthouse instance and run the following command:
```shellsession
ping the Redis instance's private IP
```
If the following information is returned, the IP cannot be pinged:
![](https://qcloudimg.tencent-cloud.cn/raw/23b44bbc2dc842c574f268dbaa407fc5.png)
2. Run the following command to install `telnet`. Take a Lighthouse instance using CentOS as an example.
```shellsession
sudo yum install telnet -y
```
3. Run the following command to test whether the interconnection is successful or not.
```shellsession
telnet the Redis instance's private IP 6379
```
If the following information is returned, the interconnection fails.
![](https://qcloudimg.tencent-cloud.cn/raw/99d63650fc4d1245d5b231e69e43b684.png)
3. Associate with a CCN as instructed in [Applying for associating with a CCN](#association).
 Associate the VPC of TencentDB for Redis with the CCN instance as instructed in [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064). 
 4. Log in to the Lighthouse instance and run the following command:
```shellsession
telnet the Redis instance's private IP 6379
``` If the following information is returned, the interconnection succeeds.
![](https://qcloudimg.tencent-cloud.cn/raw/b04377fe72b814b84bccefdeac6eb847.png)
5. Connect the Lighthouse instance to a Redis instance as instructed in [Connecting to TencentDB for Redis Instance](https://intl.cloud.tencent.com/document/product/239/9897).

:::
</dx-accordion>
