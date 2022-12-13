Gateway traffic monitoring enables you to monitor and control the bandwidth between private IPs and the gateway.
Gateway traffic monitoring fine-grains and visualizes traffic management to help you stay on top of the gateway traffic. Its IP-level traffic throttling capabilities help you quickly troubleshoot failures, block abnormal traffic, and safeguard key businesses.

Currently, you can enable gateway traffic monitoring in [Direct Connect](https://intl.cloud.tencent.com/document/product/216).
>?
>1. Sources of gateway traffic monitoring can be only CVM instances. The statistics of the traffic from other services to the gateway cannot be collected.
>2. Currently, gateway traffic monitoring is in beta test. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>

## Key Features
- Gateway traffic monitoring provides accurate gateway troubleshooting, which can minimize the network failure time. It enables you to query and view top N IPs in real time based on the traffic and analyzes source IPs and key metrics to help you quickly locate abnormal traffic.
- Gateway traffic monitoring provides "monitoring" and "control" at the granularity of IP-gateway. Minute-level network traffic query can be used to identify abnormal traffic that maliciously occupies bandwidth in time. Bandwidth limits can be set at the granularity of IP-gateway to guarantee the stable operation of core business.
- Gateway traffic monitoring analyzes all traffic at all times to help minimize network costs. By means of QoS, it can limit the bandwidth of non-key businesses to reduce costs when the network budget is limited.

## Use Cases
Gateway traffic monitoring is mainly used in scenarios where the gateway traffic of a company surges at night. By using smart gateway traffic monitoring, Ops personnel can trace the IPs that cause the traffic surge based on the time when the traffic surge occurs and quickly locate the root cause. In addition, it can control the bandwidth from an IP to a gateway to block abnormal traffic and protect key businesses.

## Billing
The gateway traffic monitoring feature is free of charge.

## Operation Guide
### Enabling gateway traffic monitoring details
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select **Direct Connect Gateway** on the left sidebar to enter the management page of the target gateway as needed. Here, a VPN gateway is used as an example.
3. Click the ID of the target gateway or connection to enter the details page.
4. Click the **Monitoring** tab and enable **Gateway Traffic Monitoring Details** in the top-right corner.
5. It takes 5–6 minutes to collect and publish data when the gateway traffic monitoring details feature is enabled. Then, you can view the details table below the monitoring charts.
![]()

### Setting gateway traffic monitoring details
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select **Direct Connect Gateway** on the left sidebar to enter the management page of the target gateway as needed. Here, a VPN gateway is used as an example.
3. Click the ID of the target gateway or connection to enter the details page.
4. Click the **Monitoring** tab.
5. Find the target IP address and click **Modify**.
![]()
6. Adjust the bandwidth and click **Save**.
![]()

### Viewing gateway traffic monitoring details
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select **Direct Connect Gateway** on the left sidebar to enter the management page of the target gateway as needed. Here, a VPN gateway is used as an example.
3. Click the ID of the target gateway or connection to enter the details page.
4. Click the **Monitoring** tab.
5. Click **View Restricted IP** in the top-right corner of the gateway traffic monitoring details table.
![]()
