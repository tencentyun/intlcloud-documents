> Security Groups can be associated with CVMs, ENIs, cloud databases and CLBs. In this document, we use CVMs for example.
>

## Scenario
A security groups can be associated with one or more CVMs for network access control. They are an important part of CVM network security measures. You can associate your CVM with one or more security groups if necessary. The following are detailed instructions.

##  Prerequisites
You should already have an CVM instance created before starting.

## Directions
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the left sidebar, select **[Security Group](https://console.cloud.tencent.com/cvm/securitygroup)**. The Security Group page then appears.
3. Select the desired region and find the security group.
4. Under **Operations**, click **Manage Instances** that corresponds to the desired security group. The **Bind with Instance** page then appears.
5. Click **Add Instances**. The **Add Instances** page then appears.
6. Select desired instances and click **OK** to add.

## See Also
- You can check all security groups in a specific region. 
See [Viewing Security Groups](https://intl.cloud.tencent.com/document/product/213/34828).
- If you want disassociate a CVM instance with one or more security groups, you can remove it from the security group. 
See [Removing From Security Groups](https://intl.cloud.tencent.com/document/product/213/34830).
- If you no longer need a security group, you can delete it. Once a security group is deleted, all rules within it are also deleted. 
See [Deleting Security Groups](https://intl.cloud.tencent.com/document/product/213/34831).

