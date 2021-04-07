 ### How does a VPN gateway work? How about its availability?
- A VPN gateway uses the network functions virtualization (NFV) and an active-active hot backup mechanism. When one server fails, automatic switchover helps ensure the normal operation of your businesses.
- Because a VPN tunnel runs on the public network, congestion, jitter, or delay on the public network may affect the VPN network. If your business is sensitive to delay and jitter, we recommend using the [Direct Connect](https://intl.cloud.tencent.com/document/product/216).

### Why does the monitoring data displayed on the VPN gateway and VPN tunnel sometimes differ?
Currently, VPN gateway and VPN tunnel collect data at a different interval. The statistical granularity of the VPN gateway is 1 minute, and that of the VPN tunnel is 10 seconds. Therefore, the statistical data shown on the monitoring page of the VPN gateway may be different from that of the VPN tunnel.

### How can I configure a VPN?
You can fully configure the IPsec VPN on the console. For more information, see [Getting Started Overview](https://intl.cloud.tencent.com/document/product/1037/32689).

### How can I create a VPN gateway?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) to create a VPN gateway as instructed in [Step 1: Create a VPN Gateway](https://intl.cloud.tencent.com/document/product/1037/32690).

### How can I create a VPN tunnel?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) to create a VPN gateway as instructed in [Step 3: Create a VPN Tunnel](https://intl.cloud.tencent.com/document/product/1037/32692).

### How can I query the VPN connection monitoring data?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) to query the VPN connection monitoring data as instructed in [Viewing Monitoring Data](https://intl.cloud.tencent.com/document/product/1037/32698).

### How can I set a VPN connection alarm?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) to set a VPN connection alarm as instructed in [Setting Alarms](https://intl.cloud.tencent.com/document/product/1037/32699).

### How can I query the VPN gateway details?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) to query the VPN gateway details as instructed in [Viewing VPN Gateway Details](https://intl.cloud.tencent.com/document/product/1037/32700).

### How can I modify the VPN tunnel configuration?
You can log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) to modify the VPN tunnel configuration as instructed in [Modifying VPN Tunnel Configuration](https://intl.cloud.tencent.com/document/product/1037/32701).

### How can I bind an Anti-DDoS instance?
You can log in to the [Anti-DDoS Pro console](https://console.cloud.tencent.com/ddos/overview) to bind an Anti-DDoS instance as instructed in [Binding an Anti-DDoS Instance](https://intl.cloud.tencent.com/document/product/1037/32705).
