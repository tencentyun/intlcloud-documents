## Types of CLB resources that can be authorized in CAM
| Resource Type | Resource Description Method in Authorization Policy |
| :-------- | -------------- |
| CLB instance |  ` qcs::clb:$region::clb/$loadbalancerid`  |
| CLB listener |   `qcs::clb:$region::listener/$loadbalancerlistenerid`  |
| CLB real server |   `qcs::cvm:$region:$account:instance/$cvminstanceid` |

Notes:
- `$region` should always be the ID of a region, and can be empty.
- `$account` should always be the AccountId of a resource owner or "\*".
- `$loadbalancerid` should always be the ID of a load balancer or "\*".

And so on…

## APIs for CLB Authorization in CAM
You can authorize the following actions for a CLB resource in CAM.
### Instance

| API Operation | Resource Description | API Description |
| :-------- | :--------| :------ |
| DescribeLoadBalancers|  Queries the CLB instance list | `*` indicates that it only authenticates the API |
| CreateLoadBalancer|  Purchases a CLB instance | `qcs:$projectid:clb:$region:$account:clb/*` |
| DeleteLoadBalancers|  Deletes CLB instances | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ModifyLoadBalancerAttributes|  Modifies the attributes of a CLB instance | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ModifyForwardLBName|  Renames a CLB instance | `qcs::clb:$region:$account:clb/$loadbalancerid` |

### Listener

| API Operation | Resource Description | API Description |
| :-------- | :---------| :------ |
|DeleteLoadBalancerListeners|Deletes CLB listeners| `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/$loadbalancerlistenerid` |
|DescribeLoadBalancerListeners|Gets the CLB listener list|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/*` |
|ModifyLoadBalancerListener|Modifies the attributes of a CLB listener|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/$loadbalancerlistenerid` |
|CreateLoadBalancerListeners|Creates CLB listeners|`qcs::clb:$region:$account:clb/$loadbalancerid` |
|DeleteForwardLBListener|Deletes a CLB listener (layer-4 and layer-7)|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/$loadbalancerlistenerid` |
|ModifyForwardLBSeventhListener|Modifies the attributes of a layer-7 CLB listener|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/$loadbalancerlistenerid` |
|ModifyForwardLBFourthListener|Modifies the attributes of a layer-4 CLB listener|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/$loadbalancerlistenerid` |
|DescribeForwardLBListeners|Queries the CLB listener list|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/*` |
|CreateForwardLBSeventhLayerListeners|Creates layer-7 CLB listeners|`qcs::clb:$region:$account:clb/$loadbalancerid` |
|CreateForwardLBFourthLayerListeners|Creates layer-4 CLB listeners|`qcs::clb:$region:$account:clb/$loadbalancerid` |

### CLB domain name and URL

| API Operation | Resource Description | API Description |
| :-------- | --------| :------ |
|ModifyForwardLBRulesDomain|Modifies the domain name of a CLB listener’s forwarding rule|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/$loadbalancerlistenerid` |
|CreateForwardLBListenerRules|Creates forwarding rules for a CLB listener|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/$loadbalancerlistenerid` |
|DeleteForwardLBListenerRules|Deletes the forwarding rules of a layer-7 CLB listener|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/$loadbalancerlistenerid` |
|DeleteRewrite|Deletes the redirection between forwarding rules of CLB instances|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/$sourceloadbalancerlistenerid` `qcs::clb:$region:$account:listener/$targetloadbalancerlistenerid` |
|ManualRewrite|Manually adds the redirection between forwarding rules of CLB instances| `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/$sourceloadbalancerlistenerid` `qcs::clb:$region:$account:listener/$targetloadbalancerlistenerid` |
|AutoRewrite|Auto-generates the redirection between forwarding rules of CLB instances|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/$loadbalancerlistenerid` |

### Real server

| API Operation | Resource Description | API Description |
| :-------- | :--------| :------ |
|ModifyLoadBalancerBackends| Modifies the real server weight of a CLB instance|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$loadbalancerlistenerid`|
|DescribeLoadBalancerBackends| Gets the list of real servers bound to a CLB instance|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/*` |
|DeregisterInstancesFromLoadBalancer |Unbinds a real server|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid`|
|RegisterInstancesWithLoadBalancer| Binds a real server to a CLB instance|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid`|
|DescribeLBHealthStatus| Queries the health status of a CLB instance|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/*` |
|ModifyForwardFourthBackendsPort| Modifies the CVM port of a layer-4 listener’s forwarding rule|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/$loadbalancerlistenerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
|ModifyForwardFourthBackendsWeight| Modifies the CVM weight of a layer-4 listener’s forwarding rule|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/$loadbalancerlistenerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
|RegisterInstancesWithForwardLBSeventhListener| Binds a CVM to the forwarding rule of a layer-7 CLB listener|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/$loadbalancerlistenerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
|RegisterInstancesWithForwardLBFourthListener| Binds a CVM to the forwarding rule of a layer-4 CLB listener|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/$loadbalancerlistenerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
|DeregisterInstancesFromForwardLBFourthListener|Unbinds the CVM from the forwarding rule of a layer-4 CLB listener|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/$loadbalancerlistenerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
|DeregisterInstancesFromForwardLB| Unbinds the CVM from the forwarding rule of a layer-7 CLB listener|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/$loadbalancerlistenerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
|ModifyForwardSeventhBackends| Modifies the CVM weight of a layer-7 CLB listener’s forwarding rule|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid`|
|ModifyForwardSeventhBackendsPort| Modifies the CVM port of a layer-7 listener’s forwarding rule|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/$loadbalancerlistenerid` `qcs::cvm:$region:$account:instance/$cvminstanceid`|
|DescribeForwardLBBackends |Queries the CVM list of a CLB instance|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/*`|
|DescribeForwardLBHealthStatus|Queries the health check status of a CLB instance|`qcs::clb:$region:$account:clb/*`  |
|ModifyLoadBalancerRulesProbe| Modifies the health check and forwarding path of a CLB listener’s forwarding rule|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::clb:$region:$account:listener/$loadbalancerlistenerid` |


