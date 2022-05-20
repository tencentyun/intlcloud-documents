After creating a NAT gateway, you can follow the directions to manage the EIPs of the gateway.

## Directions
1. Log in to the [**NAT Gateway console**](https://console.cloud.tencent.com/vpc/nat?fromNav).
2. Click the ID of the target NAT gateway to go to its details page.
3. Click the **Bind EIP** tab. On this tab, you can view the EIPs bound to the NAT gateway and manage them.
![]()

### Binding EIPs
>?
>- Loads are automatically balanced if the NAT gateway is bound to multiple EIPs.
>- Currently, you can bind the existing EIPs only. To bind more EIPs, create them first in the [Public IP console](https://console.cloud.tencent.com/cvm/eip).
>
1. Click **Bind EIP** on the top of the tab.
<img src="" width="70%">
2. In the **Select IP** drop-down list, select the EIP or EIPs to be bound, and then click **OK**.
<img src="" width="70%">
3. Click **OK**.


### Adjusting the bandwidth of the EIP
1. Find the target EIP, click **Adjust bandwidth** under the operation column.
![]()
2. Adjust the bandwidth of the target in the pop-up window, and then click **OK**.
<img src="" width="70%">

### Unbinding EIPs
>? When the NAT gateway is bound with only one EIP, the unbinding is not supported.
>
1. Find the target EIP, click **Unbind** under the operation column.
![]()
2. In the **Confirm unbinding** pop-up window, click **OK**.
<img src="" width="70%">
