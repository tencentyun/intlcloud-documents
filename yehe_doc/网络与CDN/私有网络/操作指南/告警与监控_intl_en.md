By configuring alarm policies, you can monitor the status of resources on a VPC, such as NAT gateway, VPN gateway, direct connect gateway, EIP, etc., so as to discover the abnormal running of cloud resources in time, locate and solve problems ASAP.

## Configuring an Alarm Policy
1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/overview).
2. Select **Alarm Configuration** > **Alarm Policy** in the left sidebar to enter the alarm policy configuration page.
3. Click **Create**, enter a policy name, select a VPC cloud resource to be configured for policy type, such as **VPC** > **EIP**, and then configure alarm rules and alarm notifications.
![]()
4. Click **Complete**. You can see the set alarm policy in the alarm policy list.
>? To delete an alarm policy, you need to first unbind all resources from it.
>
5. When an alarm is triggered, you will receive the alarm notification through the selected alarm channel (SMS / email/ Message Center, etc.).

Alarm policy configurations for different cloud resources are detailed below:
- Direct Connect: [Configuring Alarm Policies](https://intl.cloud.tencent.com/document/product/216/38402) 
- NAT Gateway: [Setting Alarms](https://intl.cloud.tencent.com/document/product/1015/30242) 
- VPN Connection: [Setting Alarms](https://intl.cloud.tencent.com/document/product/1037/32699) 

## Viewing Monitoring Information
You can view the monitoring information of the corresponding cloud resources in the VPC console to help you troubleshoot the network failures. See:
- Direct Connect: [Viewing Monitoring Data](https://intl.cloud.tencent.com/document/product/216/38401) 
- CCN: [View Monitoring Information](https://intl.cloud.tencent.com/document/product/1003/30071) 
- NAT Gateway: [Viewing Monitoring Information](https://intl.cloud.tencent.com/document/product/1015/30241) 
- Peering Connection: [Viewing Monitoring Data of Network Traffic Over a Cross-region Peering Connection](https://intl.cloud.tencent.com/document/product/553/18842) 
- VPN Connection: [Viewing Monitoring Data](https://intl.cloud.tencent.com/document/product/1037/32698) 
