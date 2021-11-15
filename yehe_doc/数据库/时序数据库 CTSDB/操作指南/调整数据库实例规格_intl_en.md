CTSDB supports flexible instance node specifications. You can elastically adjust the specifications of instance nodes according to your actual business conditions (at the initial stage, at the rapid development stage, during peak hours, or during off-peak hours), so as to better meet your needs such as full utilization of resources and real-time cost optimization.

## Configuration Adjustment Rules
 1. You can adjust the configuration of a CTSDB instance only when it is in normal status (Running) and is not executing any tasks.
 2. You cannot cancel a configuration adjustment operation in progress.
 3. The name, access IP, and access port of the instance remain unchanged after configuration adjustment.
 4. Configuration adjustment may cause data migration. During data migration, the instance can be accessed normally, and the business will not be affected.
 5. Instance switch may be needed after configuration adjustment is completed. We recommend you configure an automatic reconnection feature for your application.
 6. During configuration adjustment, please refrain from performing certain operations such as changing the user password.

## Configuration Adjustment Method
1. Log in to the [CTSDB console](https://console.cloud.tencent.com/ctsdb) and select the target region. In the instance list, select **More** > **Adjust Configurations** in the **Operation** column.
![](https://main.qcloudimg.com/raw/212b00c1eafee6cf21e0781ac87ab9cb.png)
2. Select the specification to be upgraded to in the pop-up window and click **Submit**.
3. You will be redirected to the instance list. After the status of the instance becomes **Running**, it can be used normally.

## Fees Calculation
2. After upgrade, pay-as-you-go instances will be billed based on the new instance specifications starting from the next billing cycle.
