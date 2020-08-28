Tencent Cloud Global Application Acceleration Platform (GAAP) is a PaaS product that achieves optimal global access latency. It uses high-speed connections, cluster forwarding, and intelligent routing among global nodes to allow users in different regions to access the closest nodes, so their request traffic can be forwarded to origin servers, reducing access lag and latency.

GAAP operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|--------------|------|-------------------------------------|
| Adding origin server         | gaap | AddRealServers                      |
| Binding listener to origin server      | gaap | BindListenerRealServers             |
| Binding forwarding rule to origin server     | gaap | BindRuleRealServers                 |
| Disabling channel         | gaap | CloseProxies                        |
| Disabling security policy       | gaap | CloseSecurityPolicy                 |
| Creating HTTP listener    | gaap | CreateHTTPListener                  |
| Creating HTTPS listener   | gaap | CreateHTTPSListener                 |
| Creating channel         | gaap | CreateProxy                         |
| Enabling the domain name of connection group      | gaap | CreateProxyGroupDomain              |
| Creating the forwarding rule for listener    | gaap | CreateRule                          |
| Creating security policy       | gaap | CreateSecurityPolicy                |
| Adding security policy rule     | gaap | CreateSecurityRules                 |
| Creating TCP listener     | gaap | CreateTCPListeners                  |
| Creating UDP listener     | gaap | CreateUDPListeners                  |
| Deleting forwarding rule of domain name   | gaap | DeleteDomain                        |
| Deleting channel listener      | gaap | DeleteListeners                     |
| Deleting connection group        | gaap | DeleteProxyGroup                    |
| Deleting the forwarding rule for layer-7 listener  | gaap | DeleteRule                          |
| Deleting security policy       | gaap | DeleteSecurityPolicy                |
| Deleting security policy rule     | gaap | DeleteSecurityRules                 |
| Querying domain name list       | gaap | DescribeGlobalDomains               |
| Querying connection group and channel statistics | gaap | DescribeGroupAndStatisticsProxy     |
| Getting the domain name configuration details of connection group  | gaap | DescribeGroupDomainConfig           |
| Querying HTTP listener information  | gaap | DescribeHTTPListeners               |
| Querying HTTPS listener information | gaap | DescribeHTTPSListeners              |
| Querying listener information      | gaap | DescribeL4Listeners                 |
| Querying the origin server list of listener    | gaap | DescribeListenerRealServers         |
| Querying listener statistics    | gaap | DescribeListenerStatistics          |
| Querying the instance list of channel     | gaap | DescribeProxies                     |
| Querying channel status       | gaap | DescribeProxiesStatus               |
| Querying channel and listener statistics | gaap | DescribeProxyAndStatisticsListeners |
| Querying channel details       | gaap | DescribeProxyDetail                 |
| Querying channel details       | gaap | DescribeProxyGroupDetails           |
| Pulling connection group list      | gaap | DescribeProxyGroupList              |
| Querying connection group statistics    | gaap | DescribeProxyGroupStatistics        |
| Querying channel statistics     | gaap | DescribeProxyStatistics             |
| Querying origin server list       | gaap | DescribeRealServers                 |
| Querying the binding status of origin server     | gaap | DescribeRealServersStatus           |
| Querying the relevant origin server information of forwarding rule | gaap | DescribeRuleRealServers             |
| Querying forwarding rule information     | gaap | DescribeRules                       |
| Getting security policy details     | gaap | DescribeSecurityPolicyDetail        |
| Querying TCP listener list   | gaap | DescribeTCPListeners                |
| Querying UDP listener list   | gaap | DescribeUDPListeners                |
| Terminating channel         | gaap | DestroyProxies                      |
| Updating domain name in the forwarding rule of listener  | gaap | ModifyDomain                        |
| Modifying the domain name of connection group    | gaap | ModifyGroupDomainConfig             |
| Modifying HTTP listener configuration  | gaap | ModifyHTTPListenerAttribute         |
| Modifying HTTPS listener configuration | gaap | ModifyHTTPSListenerAttribute        |
| Modifying channel attribute       | gaap | ModifyProxiesAttribute              |
| Modifying channel configuration       | gaap | ModifyProxyConfiguration            |
| Modifying connection group attribute      | gaap | ModifyProxyGroupAttribute           |
| Modifying origin server name       | gaap | ModifyRealServerName                |
| Modifying forwarding rule information     | gaap | ModifyRuleAttribute                 |
| Modifying security policy rule     | gaap | ModifySecurityRule                  |
| Modifying TCP listener configuration   | gaap | ModifyTCPListenerAttribute          |
| Modifying UDP listener configuration   | gaap | ModifyUDPListenerAttribute          |
| Enabling channel         | gaap | OpenProxies                         |
| Enabling security policy       | gaap | OpenSecurityPolicy                  |
| Deleting origin server         | gaap | RemoveRealServers                   |
