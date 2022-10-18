## Overview
When Origin Protection is enabled, EdgeOne notifies you of the latest update of intermediate IPs of L4 proxy and site acceleration. You can sync them to the firewall rules of your origin, allowing only traffic from these IPs to your origin. 

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Select **Security Protection** > **Origin Protection** on the left sidebar.
2. On the page that appears, enable **Origin protection**. Select the resources to bind with the intermediate IPs. Click **OK**.
>? **Select resource**: Select target resources to enable Origin Protection. 

3. When origin protection is enabled:
    - You can see the current intermediate IPs. You can update your origin firewall rules accordingly.
    - You will be informed of any updates of the intermediate IPs. Once you confirm the updates and report your update progress, the latest ones will be applied to your associated resources.

## Notes
To ensure the normal running of your business, confirm and update the intermediate IPs in the console as soon as possible after you are notified.
>?If the intermediate IPs are not updated, there may be higher latency or instability issues in case of high concurrency.

## FAQs
### Why can't I enable Origin protection for my domain name?
Origin protection only supports domain names with security acceleration enabled.

### How can I enable security acceleration for a domain name?
If your EdgeOne plan supports security acceleration, you can enable advanced protection for a specific domain name in the **Enhanced configuration** card under [**DDoS Mitigation**](https://console.cloud.tencent.com/edgeone/security/ddos).

### Can I use origin protection for non-security acceleration resources?
 No. This feature is not available if your EdgeOne plan does not support security acceleration.
