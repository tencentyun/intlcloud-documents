CLB supports cloning instance. This feature allows you to easily copy the configuration of existing CLB instances, including instance attributes, listeners, security groups, and logs.
>?The feature is currently in beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>

## Restrictions
- Only cloning pay-as-you-go instances is supported.
- Classic CLB instances and CLB with Anti-DDoS Pro are not supported.
- Classic network-based instances are not supported.
- Cloning IPv6 and IPv6 NAT64 instances as well as the instances binding the IPv4 and IPv6 simultaneously is not supported.
- Cloning the instances with QUIC and port listeners is not supported.
- Cloning the instances with the target group and SCF as the real server type is not supported.
- The following settings will not be cloned and require reconfiguration: "Custom Configuration", "Redirection Configuration" and "Allow Traffic by Default in Security Group".

## Cloning Instances in Console
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb), and click **Instance Management** on the left sidebar.
2. Select a region in the upper left corner of the "Instance Management" page, find the instance to be cloned in the instance list, and click **More** > **Clone** in the Operation column on the right.
3. In the "Clone CLB" pop-up window, enter the name of the target instance and click **OK**.
![]()

## Cloning Instances via API
For more information, please see [CloneLoadBalancer](https://intl.cloud.tencent.com/document/product/214/44335).
