A dedicated tunnel is a network linkage segmentation of a connection. You can create dedicated tunnels that connect to different direct connect gateways to enable communication between your on-premises IDC and multiple VPCs. After a dedicated tunnel is created, its event alarms will be automatically configured to facilitate your monitoring and OPS of it. This document describes how to apply for a dedicated tunnel.

[](id:background)
## Background
You can access Tencent Cloud Direct Connect via your own connections and connections shared by partners.
- Access via your own connections: You can independently connect the connection with an exclusive interface from your local IDC to the Tencent Cloud access point.
- Access via connections shared by partners: You can also use our partners' connections pre-established in Tencent to access Tencent Cloud. Currently, our partners include CTCC, CMCC, CUCC, CITIC and others with A14 and A26 telecommunication qualifications.

The tunnels created on the connections vary depending on the access method.
- The tunnels created on your own connections are exclusive dedicated tunnels, which are applicable to scenarios with requirements for high-bandwidth access and exclusive access. For details, see [Exclusive Dedicated Tunnel](https://intl.cloud.tencent.com/document/product/216/48574).
- The tunnels created on our partners' connections pre-established in Tencent are shared dedicated tunnels, which are applicable to scenarios where there is no need for high-bandwidth access and the cloudification time is short. For details, see [Shared Dedicated Tunnel](https://intl.cloud.tencent.com/document/product/216/48575).

