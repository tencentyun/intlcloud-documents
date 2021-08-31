CTSDB supports flexible instance node adjustments. You can elastically adjust the number of instance nodes according to your actual business conditions (at the initial stage, at the rapid development stage, during peak hours, or during off-peak hours), so as to better meet your needs such as full utilization of resources and real-time cost optimization.

## Node Adjustment Rules
- You can adjust the nodes of a CTSDB instance only when it is in normal status (Running) and is not executing any tasks.
- You cannot cancel a node adjustment operation in progress.
- The name, access IP, and access port of the instance remain unchanged after node adjustment.
- During node adjustment, the instance can be accessed normally, and the business will not be affected.
- Instance switch may be needed after node adjustment is completed. We recommend you configure an automatic reconnection feature for your application.
- During node adjustment, please refrain from performing certain operations such as changing the user password.

## Node Adjustment Method
1. Log in to the [CTSDB console](https://console.cloud.tencent.com/ctsdb) and select the target region. In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance details page.
2. In the **Node Quantity ** section on the instance details page, click **Add Node**.
![](https://main.qcloudimg.com/raw/3ef4b65d36ee84fc168eeaadea510cff.png)
3. Select the number of nodes to be added in the pop-up window and click **Upgrade**.

## Fees Calculation
2. After upgrade, pay-as-you-go instances will be billed based on the new instance specifications starting from the next billing cycle.
