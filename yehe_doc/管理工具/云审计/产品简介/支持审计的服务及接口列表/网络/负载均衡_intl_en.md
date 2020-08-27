Tencent Cloud Load Balancer (CLB) is a secure and fast traffic distribution service. Inbound traffic can be automatically distributed to multiple CVM instances in the cloud through CLB, improving service capabilities systematically and eliminating single points of failure. CLB supports hundreds of millions of connections and tens of millions of concurrent requests, making it easy to handle high-traffic access and meet demanding business needs.

CLB operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|-----------------------|------|------------------------------------------------|
| Binding target group                 | clb  | AssociateTargetGroups                          |
| Automatically rewriting           | clb  | AutoRewrite                                    |
| Unbinding real servers in batches              | clb  | BatchDeregisterTargets                         |
| Binding real servers in batches              | clb  | BatchRegisterTargets                           |
| Creating layer-4 CLB listener            | clb  | CreateForwardLBFourthLayerListeners            |
| Creating forwarding rule for layer-7 listener         | clb  | CreateForwardLBListenerRules                   |
| Creating layer-7 CLB listener         | clb  | CreateForwardLBSeventhLayerListeners           |
| Creating CLB listener             | clb  | CreateListener                                 |
| Creating CLB instance                | clb  | CreateLoadBalancer                             |
| Creating CLB listeners             | clb  | CreateLoadBalancerListeners                    |
| Adding SNAT IP              | clb  | CreateLoadBalancerSnatIps                      |
| Creating forwarding rule for layer-7 CLB listener       | clb  | CreateRule                                     |
| Creating target group                 | clb  | CreateTargetGroup                              |
| Deleting CLB listener (layer-4 and layer-7)       | clb  | DeleteForwardLBListener                        |
| Deleting layer-7 CLB listener rule     | clb  | DeleteForwardLBListenerRules                   |
| Deleting CLB listener             | clb  | DeleteListener                                 |
| Deleting CLB instance              | clb  | DeleteLoadBalancer                             |
| Deleting CLB listeners             | clb  | DeleteLoadBalancerListeners                    |
| Deleting CLB instances                | clb  | DeleteLoadBalancers                            |
| Deleting SNAT IP              | clb  | DeleteLoadBalancerSnatIps                      |
| Deleting redirection relationship               | clb  | DeleteRewrite                                  |
| Deleting layer-7 CLB listener rule      | clb  | DeleteRule                                     |
| Deleting target group                 | clb  | DeleteTargetGroups                             |
| Unbinding CVM instance from layer-7 listener        | clb  | DeregisterInstancesFromForwardLB               |
| Unbinding instance from layer-4 CLB listener        | clb  | DeregisterInstancesFromForwardLBFourthListener |
| Unbinding real server               | clb  | DeregisterInstancesFromLoadBalancer            |
| Removing instance from target group               | clb  | DeregisterTargetGroupInstances                 |
| Unbinding real server registered with CLB listener | clb  | DeregisterTargets                              |
| Unbinding real server from classic CLB instance       | clb  | DeregisterTargetsFromClassicalLB               |
| Querying the real server information of CLB instance          | clb  | DescribeAllLBBackends                          |
| Getting the real server health status of classic CLB instance      | clb  | DescribeClassicalLBHealthStatus                |
| Getting classic CLB listener list        | clb  | DescribeClassicalLBListeners                   |
| Getting the list of real servers bound to classic CLB instance   | clb  | DescribeClassicalLBTargets                     |
| Querying associated instance               | clb  | DescribeForwardLBBackends                      |
| Querying the health check result of CLB instance        | clb  | DescribeForwardLBHealthStatus                  |
| Querying CLB listener           | clb  | DescribeForwardLBListeners                     |
| Querying the health status of CLB instance            | clb  | DescribeLBHealthStatus                         |
| Querying CLB listener list        | clb  | DescribeListeners                              |
| Getting the list of real servers of CLB instance         | clb  | DescribeLoadBalancerBackends                   |
| Getting CLB listener list           | clb  | DescribeLoadBalancerListeners                  |
| Pulling the application layer log of CLB instance           | clb  | DescribeLoadBalancerLog                        |
| Getting CLB instance list            | clb  | DescribeLoadBalancers                          |
| Querying CLB instance details           | clb  | DescribeLoadBalancersDetail                    |
| Querying redirection relationship               | clb  | DescribeRewrite                                |
| Getting the list of instances bound to target group          | clb  | DescribeTargetGroupInstances                   |
| Getting target group list               | clb  | DescribeTargetGroupList                        |
| Getting target group information               | clb  | DescribeTargetGroups                           |
| Querying the health status of real server            | clb  | DescribeTargetHealth                           |
| Querying the list of CVM instances bound to CLB instance       | clb  | DescribeTargets                                |
| Unbinding target group                 | clb  | DisassociateTargetGroups                       |
| Customizing redirection              | clb  | ManualRewrite                                  |
| Modifying the domain name in layer-7 forwarding rule           | clb  | ModifyDomain                                   |
| Modifying the domain name attribute in layer-7 listener       | clb  | ModifyDomainAttributes                         |
| Modifying the port of real server bound to layer-4 CLB listener        | clb  | ModifyForwardFourthBackendsPort                |
| Modifying the weight of real server bound to layer-4 CLB listener        | clb  | ModifyForwardFourthBackendsWeight              |
| Modifying layer-4 CLB listener attribute          | clb  | ModifyForwardLBFourthListener                  |
| Renaming application CLB instance          | clb  | ModifyForwardLBName                            |
| Modifying layer-7 listener attribute             | clb  | ModifyForwardLBSeventhListener                 |
| Modifying real server weight             | clb  | ModifyForwardSeventhBackends                   |
| Changing real server port             | clb  | ModifyForwardSeventhBackendsPort               |
| Upgrading/Degrading configuration of pay-as-you-go CLB instance            | clb  | ModifyLBNetwork                                |
| Modifying project ID                | clb  | ModifyLBProjectId                              |
| Modifying CLB listener attribute           | clb  | ModifyListener                                 |
| Modifying CLB instance attribute            | clb  | ModifyLoadBalancerAttributes                   |
| Modifying real server weight of CLB instance        | clb  | ModifyLoadBalancerBackends                     |
| Modifying CLB listener             | clb  | ModifyLoadBalancerListener                     |
| Modifying health check configuration of forwarding rule           | clb  | ModifyLoadBalancerRulesProbe                   |
| Modifying CLB listener forwarding rule      | clb  | ModifyRule                                     |
| Modifying target group attribute               | clb  | ModifyTargetGroupAttribute                     |
| Modifying instance port in target group            | clb  | ModifyTargetGroupInstancesPort                 |
| Modifying instance weight in target group            | clb  | ModifyTargetGroupInstancesWeight               |
| Modifying the port of real server bound to listener       | clb  | ModifyTargetPort                               |
| Modifying the forwarding weight of real server bound to listener     | clb  | ModifyTargetWeight                             |
| Binding instance to layer-4 CLB listener        | clb  | RegisterInstancesWithForwardLBFourthListener   |
| Binding instance to layer-7 listener           | clb  | RegisterInstancesWithForwardLBSeventhListener  |
| Binding real server to CLB instance          | clb  | RegisterInstancesWithLoadBalancer              |
| Adding instance to target group               | clb  | RegisterTargetGroupInstances                   |
| Binding real server to listener           | clb  | RegisterTargets                                |
| Binding real server to classic CLB instance        | clb  | RegisterTargetsWithClassicalLB                 |
| Replacing old certificate with new one            | clb  | ReplaceCert                                    |
| Modifying the custom configuration of CLB instance        | clb  | SetCustomizedConfigForLoadBalancer             |
| Setting CLB log service topic         | clb  | SetLoadBalancerClsLog                          |
| Setting the cross-region attribute of CLB instance           | clb  | SetLoadBalancerCrossRegion                     |
| Starting CLB logging              | clb  | SetLoadBalancerLog                             |
| Binding CLB instance to security group               | clb  | SetLoadBalancerSecurityGroups                  |
| Binding security group to CLB instance            | clb  | SetSecurityGroupForLoadbalancers               |
| Setting security group                 | clb  | SetSecurityGroups                              |
