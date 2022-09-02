By connecting CLB access logs to Cloud Log Service, you can check the access logs in a dashboard. The dashboard provides charts of multiple metrics, giving you a full picture of the load balancer. 

## Dashboard
Each log topic has its own dashboard, which contains data of following metrics. 
- PV
- UV
- Outgoing request message traffic
- Incoming response traffic
- Average request time
- Average response time
- Backend status code distribution
- Overall status code distribution
- PV/UV trend
- Outgoing/Incoming traffic trend
- Average requests/responses per minute
- P99, P95, P90, P50 access duration
- Top requested instances
- Top requested domain names

## Preparations
 Create logsets for CLB. See [Creating Logsets and Log Topics](https://intl.cloud.tencent.com/document/product/214/40509).

## Directions
1. Log in to the [CLB console](https://console.cloud.tencent.com/clb) and select **Access Logs** on the left sidebar.
2. In the **Access Log Dashboard** page, select the region and log topic to see the dashboard of this log topic.
![]()
3. (Optional) In the upper corner of the **Access Log Dashboard** page, filter logs by the CLB VIP, client IP, backend server IP and status code.

## See Also
For more information, see [Configuring Access Logs](https://intl.cloud.tencent.com/document/product/214/40509).
