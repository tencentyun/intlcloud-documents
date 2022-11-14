

### Why can't an inter-VPC firewall be enabled?
Due to issues such as route and network segment conflicts, CFW limits any firewall generating conflicts. You can fix the conflicts as instructed, and then try to enable the inter-VPC firewall again.

### What are firewall subnet and firewall route in the route table automatically created in a VPC?
After the inter-VPC firewall toggle is enabled, the firewall subnet and firewall route required for traffic introduction control will be automatically created. Please do not manually delete them to avoid effects on CFW. If you want to change the firewall subnet segment, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us.

### What subnets among VPCs will inter-VPC firewall introduce traffic for?
It depends on your inter-VPC routing configuration. CFW only introduces traffic for subnets correctly configured with inter-VPC routing.

###What if the bandwidth of inter-VPC firewall reaches the upper limit?
- The current version does not support elastic scaling because the inter-VPC firewall is deployed with exclusive resources.
- When the bandwidth of inter-VPC firewall reaches the upper limit, the firewall escape will be enabled and the firewall will be switched to the bypass mode in critical conditions, with 50% buffer bandwidth reserved to avoid effects on normal services.

>? 
>- In bypass mode, CFW does not process any traffic, and all traffic is allowed to pass.
>- Please keep your eye on CFW bandwidth alerts. In case of high bandwidth, disable the firewall feature for some networks.



