Tencent Cloud Direct Connect (DC) enables you to easily connect your organizational IDC to Tencent Cloud. You can use DC to build a private connection service completely isolated from the public network. Compared with public network, DC boasts advantages such as higher security, stability, and bandwidth and lower latency. All you need to do is connect to Tencent Cloud through one ISP connection. After that, you can quickly create multiple dedicated tunnels to access your computing resources deployed in Tencent Cloud, implementing a flexible and reliable hybrid cloud deployment. In addition, various billing modes of DC can help you save connection usage costs in different scenarios.

DC operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|-----------|------|---------------------------------|
| Creating connection    | dc   | CreateDirectConnect             |
| Creating dedicated tunnel for internet access | dc   | CreatePublicDirectConnectTunnel |
| Deleting connection    | dc   | DeleteDirectConnect             |
| Querying connection access point | dc   | DescribeAccessPoints            |
| Getting connection list  | dc   | DescribeDirectConnects          |
| Updating connection attribute  | dc   | ModifyDirectConnectAttribute    |

