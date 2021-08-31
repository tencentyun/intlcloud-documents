## Types of CLB Resources Authorizable in CAM
| Resource Type | Resource Description in Authorization Policy |
| :-------- | -------------- |
| CLB instance |  ` qcs::clb:$region::clb/$loadbalancerid`  |
| CLB real server | `qcs::cvm:$region:$account:instance/$cvminstanceid` |

Here:
- `$region` should always be the ID of a region and can be empty.
- `$account` should always be the `AccountId` of the resource owner or `*`.
- `$loadbalancerid` should always be the ID of a CLB instance or `*`.

And so on...

## APIs Authorizable for CLB in CAM
You can authorize the following actions for a CLB resource in CAM.
### Instance

| API Operation | Resource Description | API Description |
| :-------- | :--------| :------ |
| DescribeLoadBalancers |  Queries CLB instance list | `*` indicates to only authenticate the API |
| CreateLoadBalancer |  Purchases CLB instance | `qcs:$projectid:clb:$region:$account:clb/*` |
| DeleteLoadBalancers |  Deletes CLB instance | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ModifyLoadBalancerAttributes |  Modifies the attributes of CLB instance | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ModifyForwardLBName |  Renames CLB instance | `qcs::clb:$region:$account:clb/$loadbalancerid` |

### Listener

| API Operation | Resource Description | API Description |
| :-------- | :---------| :------ |
| DeleteLoadBalancerListeners | Deletes CLB listener| `qcs::clb:$region:$account:clb/$loadbalancerid`  |
| DescribeLoadBalancerListeners | Gets CLB listener list | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ModifyLoadBalancerListener | Modifies the attributes of CLB listener | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| CreateLoadBalancerListeners | Creates CLB listener | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| DeleteForwardLBListener | Deletes CLB listener (layer-4 and layer-7) | `qcs::clb:$region:$account:clb/$loadbalancerid`  |
| ModifyForwardLBSeventhListener | Modifies the attributes of CLB layer-7 listener | `qcs::clb:$region:$account:clb/$loadbalancerid`  |
| ModifyForwardLBFourthListener | Modifies the attributes of CLB layer-4 listener | `qcs::clb:$region:$account:clb/$loadbalancerid`  |
| DescribeForwardLBListeners | Queries CLB listener list | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| CreateForwardLBSeventhLayerListeners | Creates layer-7 CLB listener | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| CreateForwardLBFourthLayerListeners | Creates layer-4 CLB listener| `qcs::clb:$region:$account:clb/$loadbalancerid` |

### CLB domain name and URL

| API Operation | Resource Description | API Description |
| :-------- | --------| :------ |
| ModifyForwardLBRulesDomain | Modifies the domain name of CLB listener's forwarding rule | `qcs::clb:$region:$account:clb/$loadbalancerid`  |
| CreateForwardLBListenerRules |Creates CLB listener forwarding rule | `qcs::clb:$region:$account:clb/$loadbalancerid`  |
| DeleteForwardLBListenerRules | Deletes layer-7 CLB listener rule | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| DeleteRewrite | Deletes the redirect relationship of CLB instance's forwarding rule | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ManualRewrite | Manually adds the redirect relationship of CLB instance's forwarding rule | `qcs::clb:$region:$account:clb/$loadbalancerid`  |
| AutoRewrite | Automatically generates the redirect relationship of CLB instance's forwarding rule | `qcs::clb:$region:$account:clb/$loadbalancerid`  |

### Real server

| API Operation | Resource Description | API Description |
| :-------- | :--------| :------ |
| ModifyLoadBalancerBackends | Modifies the real server weight of CLB instance | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| DescribeLoadBalancerBackends | Gets the list of real servers bound to CLB instance | `qcs::clb:$region:$account:clb/$loadbalancerid`  |
| DeregisterInstancesFromLoadBalancer | Unbinds real server | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| RegisterInstancesWithLoadBalancer | Binds real server to CLB instance | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| DescribeLBHealthStatus | Queries CLB health status | `qcs::clb:$region:$account:clb/$loadbalancerid`  |
| ModifyForwardFourthBackendsPort | Modifies CVM instance port in layer-4 listener's forwarding rule | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| ModifyForwardFourthBackendsWeight | Modifies CVM instance weight in layer-4 listener's forwarding rule | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| RegisterInstancesWithForwardLBSeventhListener | Binds CVM instance to CLB layer-7 listener's forwarding rule | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| RegisterInstancesWithForwardLBFourthListener | Binds CVM instance to CLB layer-4 listener's forwarding rule | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| DeregisterInstancesFromForwardLBFourthListener | Unbinds CVM instance from CLB layer-4 listener's forwarding rule | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| DeregisterInstancesFromForwardLB | Unbinds CVM instance from CLB layer-7 listener's forwarding rule | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| ModifyForwardSeventhBackends | Modifies CVM instance weight in layer-7 listener's forwarding rule | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| ModifyForwardSeventhBackendsPort | Modifies CVM instance port in layer-7 listener's forwarding rule | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| DescribeForwardLBBackends | Queries the CVM instance list of CLB instance | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/*` |
| DescribeForwardLBHealthStatus | Queries CLB health check status | `qcs::clb:$region:$account:clb/*`  |
| ModifyLoadBalancerRulesProbe | Modifies the health check and forwarding path of CLB listener's forwarding rule | `qcs::clb:$region:$account:clb/$loadbalancerid` |


