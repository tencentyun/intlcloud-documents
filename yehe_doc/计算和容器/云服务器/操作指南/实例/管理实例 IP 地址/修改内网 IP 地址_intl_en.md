## Scenario

You can modify the private IP of a CVM instance in VPC directly on the console or by changing the subnet of the CVM instance. This document describes how to modify the private IP of a CVM instance in the VPC console.
For details on changing the subnet, see [Change Instance Subnet](http://intl.cloud.tencent.com/document/product/213/16565).

## Limits

- Modifying the primary IP of a primary ENI may cause the CVM to restart.
- The primary IP of a secondary ENI cannot be modified.

## Directions

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. Select the region of the instance whose private IP you want to modify, and click the instance ID/name to enter its details page.
3. On the instance details page, select the [ENI] tab and click <img src = "https://main.qcloudimg.com/raw/57a0c76b72cd97bd80bf857cd30c867a.png" style = "margin: 0;"> to expand the primary ENI.
4. In the primary ENI operation list, click **Modify Primary IP**.
5. In the “Modify Primary IP” window that pops up, enter the new IP and then click **OK**. It takes effect after the instance is restarted.
>! You can only enter private IP in the current subnet CIDR.
>

