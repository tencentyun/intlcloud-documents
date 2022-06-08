You can specify different service level for different ENIs. When bandwidth congestion occurs, this can ensure that the key services with high priority be forwarded first.
There are four service levels, Gold, Silver, Bronze and Default, ranking by priority for traffic forwarding. You can keep it as Default for general usage.
>?
>- The service level defaults to "Default".
>- ENI is a private network resource. The service level is only applied to underlying traffic service and is irrelevant to the billing.
>
## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Choose **IP and ENI** > **ENI** in the left sidebar to go to the ENI list page.
3. Locate the target ENI. Click **More** > **Set service level** in the **Operation** column.
 ![]()
4. Choose a service level from the drop-down list. Click **OK**.
![]()
5. To set the same service level for multiple ENIs, you can select multiple ENIs and click **Set service level** at the top.
 ![]()
6. Click **OK**.
 ![]()
