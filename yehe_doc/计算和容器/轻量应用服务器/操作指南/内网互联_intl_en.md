## Overview
Lighthouse uses the VPC automatically assigned by Tencent Cloud for network isolation. By default, Lighthouse instances cannot interconnect with other Tencent Cloud resources in VPCs such as CVM and TencentDB over the private network, and their interconnection needs to be implemented by associating a CCN instance. This feature is applicable in the following scenarios:
 - Lighthouse access to CVM.
 - Lighthouse access to TencentDB.

<dx-alert infotype="explain" title="">
- Different Lighthouse instances in the same region under the same account are interconnected over the private network by default. For more information on Lighthouse connectivity over the private network, see [Region and Network Connectivity](https://intl.cloud.tencent.com/document/product/1103/41266).
- Lighthouse and COS in the same region are interconnected over the private network by default with no need to be interconnected over CCN.
</dx-alert>

This document describes how to associate/disassociate an instance with/from CCN in the Lighthouse console. For more information on CCN, see [Overview](https://intl.cloud.tencent.com/document/product/1003/30049).

## Notes
- The private network interconnection feature of Lighthouse is free of charge. You only need to pay attention to CCN billing information. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1003/30053). Connection within the same region at a bandwidth of below 5 Gbps is free of charge. To implement cross-region private network interconnection, you need to purchase [non-cross-region bandwidth](https://intl.cloud.tencent.com/document/product/1003/38894) in CCN.
- Lighthouse does not support cross-region private network interconnection by associating a CCN instance, even if cross-region bandwidth has been purchased for the instance.
- Under the same account:
  - All Lighthouse instances in the same region are in the same VPC. A VPC can be associated with only one CCN instance.
  - Lighthouse instances in different regions are in different VPCs, which need to be associated with CCN instances separately.
- If there are no Lighthouse instances in a region, you cannot associate a CCN instance in that region.

## Directions

### Applying for CCN association[](id:association)
1. Log in to the Lighthouse console and select <b>[Private Network Interconnection](https://console.cloud.tencent.com/lighthouse/ccn/index)</b> on the left sidebar.
2. Select **Associate CCN Instance** for the target region as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/fdf2d7e60a095e95303e226c693cbfa2.png)
3. In the **Associate CCN Instance** pop-up window, select the target CCN instance and click **OK** to submit the association application.
<dx-alert infotype="notice" title="">
- Only CCN instances under the same account can be associated with.
- After submitting the association application, log in to the [CCN console](https://console.cloud.tencent.com/vpc/ccn) in seven days to approve the application; otherwise, the application will expire, and you need to apply for association again.
</dx-alert>
4. Log in to the [CCN console](https://console.cloud.tencent.com/vpc/ccn) and select a CCN instance ID to enter the instance details page.
5. On the CCN instance details page, select **Approve** on the right of the target association application.
Remarks "Lighthouse VPC" will be added to the VPC instance of Lighthouse by default. Select the correct instance as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/363bd10b3f88e60e86da7e3e58c2e6f8.png)
6. In the pop-up window, click **OK** to complete association. On the private network interconnection page, the region status will become **Connected**.
You can associate Tencent Cloud resources such as CVM and TencentDB instances to CCN to implement private network interconnection. For more information, see [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).
<dx-alert infotype="notice" title="">
After the association, you need to go to the [CCN console](https://console.cloud.tencent.com/vpc/ccn) to view the routing information and check whether the new route takes effect. If there is any CIDR block conflict, the route may be invalid. For more information, see [Viewing Routing Information](https://intl.cloud.tencent.com/document/product/1003/30066).
</dx-alert>



### Disassociating CCN instance[](id:disassociate)
You can disassociate a CCN instance when the CCN association application status is "Applying", "Expired", or "Connected". If the status is "Connected", disassociation will interrupt the connections of all instances in the current region to other VPCs in CCN. Perform the following operations after confirming that they will not affect your business:
1. Log in to the Lighthouse console and select <b>[Private Network Interconnection](https://console.cloud.tencent.com/lighthouse/ccn/index)</b> on the left sidebar. 
2. Select **Disassociate** of the target region as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/565a447f7c1b5b9a147cb7706c1c634e.png)
3. In the **Disassociate from CCN** pop-up window, click **OK**.

## Examples
<dx-accordion>
::: Example 1: Lighthouse and CVM interconnection over private network
#### Scenario
The Lighthouse and CVM instances in the Guangzhou region are not interconnected over the private network by default and need to be associated with CCN for interconnection.

#### Steps
 1. Log in to the Lighthouse instance and run the following command:
```
ping CVM instance's private IP
```
If the following information is returned, the IP cannot be pinged:
![](https://main.qcloudimg.com/raw/49e76f62b5f7ae7e6fb504bf92b842a7.png)
 2. Associate CCN as instructed in [Applying for CCN association](#association).
 In addition, you need to associate the VPC of the CVM instance with CCN as instructed in [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064). 
 3. Log in to the Lighthouse instance and run the following command:
```
ping CVM instance's private IP
```
If the following information is returned, the IP can be pinged and the private networks have been interconnected:
![](https://main.qcloudimg.com/raw/b487ec4b7ae4be87059bd13db2f5f9b4.png)
:::
::: Example 2: Lighthouse and TencentDB for MySQL interconnection over private network
#### Scenario
The Lighthouse and TencentDB for MySQL instances in the Guangzhou region are not interconnected over the private network by default and need to be associated with CCN for interconnection.

#### Steps
1. Log in to the Lighthouse instance and run the following command to install `telnet`:
```shell
sudo yum install telnet -y
```
2. Run the following command to test whether the private networks are interconnected:
```
telnet TencentDB for MySQL instance's private IP 3306
``` If the following information is returned, the interconnection cannot be made.
![](https://main.qcloudimg.com/raw/e4faffa0bf9bb3448296d3bcae1c6dec.png)
3. Associate CCN as instructed in [Applying for CCN association](#association).
 In addition, you need to associate the VPC of the TencentDB for MySQL instance with CCN as instructed in [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064). 
4. Log in to the Lighthouse instance and run the following command:
```
telnet TencentDB for MySQL instance's private IP 3306
``` If the following information is returned, the private networks have been interconnected:
![](https://main.qcloudimg.com/raw/98f0b235240869f954b7dcfa23df202c.png)
:::
</dx-accordion>
