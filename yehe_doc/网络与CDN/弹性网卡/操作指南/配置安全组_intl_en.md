The secondary ENI can be bound with one or more security groups, which implement access control on the in/outbound traffic of the ENI. You need to bind the security group to the created secondary ENI according to your business situation. The ENI can be bound with the same security groups as or different ones from the CVM instances.
This document describes how to bind a security group to or unbind it from the secondary ENI.



## Binding security groups[](id:group)
### Prerequisites
You've created the security group(s) as instructed in [Creating a security group](https://intl.cloud.tencent.com/document/product/215/35506).

### Operation Guide
1. Log in to the [ENI console](https://console.cloud.tencent.com/vpc/eni?rid=1).
2 Click the ID of the ENI to which the security group needs to be bound.
3. Click **Bind** in the **Associate security group** tab.
    ![]()
4. In the **Configure security group** pop-up interface, check your created security group(s), and click **OK**. When multiple security groups are bound, the higher the security group is, the higher its priority will be, and it will be matched earlier.
![]()


## Unbinding security groups
>! It is recommended that you reserve at least one security group for an ENI.
>
### Operation Guide
1. Log in to the [ENI console](https://console.cloud.tencent.com/vpc/eni?rid=1).
2 Click the ID of the ENI from which the security group needs to be unbound.
3. In the ENI details page, click **Associate security group** tab, and then click **Unbind** in the **operation** column of the **Bound security groups** list.
   ![]()
4. In the pop-up window, click **OK**.
![]()
