## General APIs
<table>
<thead>
<tr>
<th width="30%">API Name</th>
<th width="40%">Action</th>
<th width="30%">Feature</th>
</tr>
</thead>
<tbody><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/4007" target="_blank">DescribeLoadBalancersTaskResult</a></td>
<td >DescribeLoadBalancersTaskResult</td>
<td >Queries the execution result of an async CLB API.</td>
</tr>
<tr>
<td ><a href="https://intl.cloud.tencent.com/document/product/214/1254" target="_blank">CreateLoadBalancer</a></td>
<td>CreateLoadBalancer</td>
<td>Purchases a CLB instance.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/1328" target="_blank">InquiryLBPriceAll</a></td>
<td>InquiryLBPriceAll</td>
<td>Queries the price of CLB instances.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/1261" target="_blank">DescribeLoadBalancers</a></td>
<td>DescribeLoadBalancers</td>
<td>Queries the list of CLB instances.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/api/214/1257" target="_blank">DeleteLoadBalancers</a></td>
<td>DeleteLoadBalancers</td>
<td>Deletes one or more CLB instance.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/8801" target="_blank">GetMonitorData</a></td>
<td>GetMonitorData</td>
<td>Queries monitoring data of CLB instances.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/6045" target="_blank">ReplaceCert</a></td>
<td>ReplaceCert</td>
<td>Changes the certificate of a CLB instance.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/6046" target="_blank">GetCertListWithLoadBalancer</a></td>
<td>GetCertListWithLoadBalancer</td>
<td>Queries CLB instances associated with the specified certificate.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/37069" target="_blank">CloneLB</a></td>
<td>CloneLB</td>
<td>Clones a CLB instance.</td>
</tr>
</tbody></table>

## Classic CLB APIs
### Instance APIs

<table>
<thead>
<tr>
<th width="30%">API Name</th>
<th width="40%">Action</th>
<th width="30%">Feature</th>
</tr>
</thead>
<tbody><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/1263" target="_blank">ModifyLoadBalancerAttributes</a></td>
<td>ModifyLoadBalancerAttributes</td>
<td>Modifies the attributes of a specified CLB instance, including the CLB instance name.</td>
</tr>
</tbody></table>

### Listener APIs

<table>
<thead>
<tr>
<th width="30%">API Name</th>
<th width="40%">Action</th>
<th width="30%">Feature</th>
</tr>
</thead>
<tbody><tr>
<td><a href="https://intl.cloud.tencent.com/document/api/214/1255" target="_blank">CreateLoadBalancerListeners</a></td>
<td>CreateLoadBalancerListeners</td>
<td>Creates one or more CLB listeners for the specified CLB instance. A CLB listener provides request forwarding protocols, ports, and health check policies.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/api/214/1260" target="_blank">DescribeLoadBalancerListeners</a></td>
<td>DescribeLoadBalancerListeners</td>
<td>Obtains the list of listeners for the specified CLB instance, including unique ID, name, port, and health check policy.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/api/214/1256" target="_blank">DeleteLoadBalancerListeners</a></td>
<td>DeleteLoadBalancerListeners</td>
<td>Deletes listeners for the specified CLB instance.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/api/214/3601" target="_blank">ModifyLoadBalancerListener</a></td>
<td>ModifyLoadBalancerListener</td>
<td>Modifies the attributes of a CLB listener, including the listener name and health check policy.</td>
</tr>
</tbody></table>

### Real server APIs
<table>
<thead>
<tr>
<th width="30%">API Name</th>
<th width="40%">Action</th>
<th width="30%">Feature</th>
</tr>
</thead>
<tbody><tr>
<td><a href="https://intl.cloud.tencent.com/document/api/214/1265" target="_blank">RegisterInstancesWithLoadBalancer</a></td>
<td>RegisterInstancesWithLoadBalancer</td>
<td>Binds the specified CVMs to a specified CLB instance.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/api/214/1259" target="_blank">DescribeLoadBalancerBackends</a></td>
<td>DescribeLoadBalancerBackends</td>
<td>Obtains the list of CVMs bound to the CLB instance with the specified <em>LoadBalanceId</em>.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/api/214/1264" target="_blank">ModifyLoadBalancerBackends</a></td>
<td>ModifyLoadBalancerBackends</td>
<td>Modifies the weights of CVMs bound to a CLB instance.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/api/214/1258" target="_blank">DeregisterInstancesFromLoadBalancer</a></td>
<td>DeregisterInstancesFromLoadBalancer</td>
<td>Unbinds CVMs from a CLB instance.</td>
</tr>
</tbody></table>

### Health check APIs
<table>
<thead>
<tr>
<th width="30%">API Name</th>
<th width="40%">Action</th>
<th width="30%">Feature</th>
</tr>
</thead>
<tbody><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/1326" target="_blank">DescribeLBHealthStatus</a></td>
<td>DescribeLBHealthStatus</td>
<td>Queries the health status of a CLB instance.</td>
</tr>
</tbody></table>

## Cloud Load Balancer APIs
>?The following CLB APIs have been updated to version 3.0. These legacy APIs may be deprecated and is currently not displayed on the left sidebar. We recommend using [CLB API 3.0](https://intl.cloud.tencent.com/document/product/214/33789), which is more standardized and has a significantly reduced access latency.

### CLB instance APIs
<table>
<thead>
<tr>
<th width="30%">API Name</th>
<th width="40%">Action</th>
<th width="30%">Feature</th>
</tr>
</thead>
<tbody><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/13295" target="_blank">ModifyForwardLBName</a></td>
<td>ModifyForwardLBName</td>
<td>Modifies the name of a CLB instance.</td>
</tr>
</tbody></table>

### Listener APIs
<table>
<thead>
<tr>
<th width="30%">API Name</th>
<th width="40%">Action ID</th>
<th width="30%">Feature</th>
</tr>
</thead>
<tbody><tr>
<td>DescribeForwardLBListeners</td>
<td>DescribeForwardLBListeners</td>
<td>Queries CLB listeners.</td>
</tr>
<tr>
<td>CreateForwardLBSeventhLayerListeners</td>
<td>CreateForwardLBSeventhLayerListeners</td>
<td>Creates one or more Layer-7 listeners.</td>
</tr>
<tr>
<td>CreateForwardLBFourthLayerListeners</td>
<td>CreateForwardLBFourthLayerListeners</td>
<td>Creates one or more Layer-4 listener.</td>
</tr>
<tr>
<td>ModifyForwardLBFourthListener</td>
<td>ModifyForwardLBFourthListener</td>
<td>Modifies the attributes of a CLB Layer-4 listener.</td>
</tr>
<tr>
<td>ModifyForwardLBSeventhListener</td>
<td>ModifyForwardLBSeventhListener</td>
<td>Modifies the attributes of a CLB Layer-7 listener.</td>
</tr>
<tr>
<td>DeleteForwardLBListener</td>
<td>DeleteForwardLBListener</td>
<td>Deletes a CLB listener.</td>
</tr>
</tbody></table>


### Forwarding rule APIs
<table>
<thead>
<tr>
<th width="30%">API Name</th>
<th width="40%">Action ID</th>
<th width="30%">Feature</th>
</tr>
</thead>
<tbody><tr>
<td>CreateForwardLBListenerRules</td>
<td>CreateForwardLBListenerRules</td>
<td>Creates forwarding rules of a CLB Layer-7 listener.</td>
</tr>
<tr>
<td>ModifyForwardLBRulesDomain</td>
<td>ModifyForwardLBRulesDomain</td>
<td>Modifies the domain name under a CLB Layer-7 listener.</td>
</tr>
<tr>
<td>ModifyLoadBalancerRulesProbe</td>
<td>ModifyLoadBalancerRulesProbe</td>
<td>Modifies the health check and forwarding path for the forwarding rules of a CLB Layer-7 listener.</td>
</tr>
<tr>
<td>DeleteForwardLBListenerRules</td>
<td>DeleteForwardLBListenerRules</td>
<td>Deletes forwarding rules of a CLB Layer-7 listener.</td>
</tr>
</tbody></table>

### CVM APIs

<table>
<thead>
<tr>
<th width="30%">API Name</th>
<th width="40%">Action ID</th>
<th width="30%">Feature</th>
</tr>
</thead>
<tbody><tr>
<td>DescribeForwardLBBackends</a></td>
<td>DescribeForwardLBBackends</td>
<td>Obtains the list of CVMs bound to a CLB instance.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/8989" target="_blank">RegisterInstancesWithForwardLBFourthListener</a></td>
<td>RegisterInstancesWithForwardLBFourthListener</td>
<td>Binds CVMs to the forwarding rules of a CLB Layer-4 listener.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/8988" target="_blank">RegisterInstancesWithForwardLBSeventhListener</a></td>
<td>RegisterInstancesWithForwardLBSeventhListener</td>
<td>Binds CVMs to the forwarding rules of a CLB Layer-7 listener.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/8981" target="_blank">ModifyForwardFourthBackendsWeight</a></td>
<td>ModifyForwardFourthBackendsWeight</td>
<td>Modifies the weight of CVMs bound to a Layer-4 listener.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/8978" target="_blank">ModifyForwardSeventhBackends</a></td>
<td>ModifyForwardSeventhBackends</td>
<td>Modifies the weight of CVMs bound to a Layer-7 listener.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/8984" target="_blank">ModifyForwardFourthBackendsPort</a></td>
<td>ModifyForwardFourthBackendsPort</td>
<td>Modifies ports of CVMs bound to a Layer-4 listener.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/8979" target="_blank">ModifyForwardSeventhBackendsPort</a></td>
<td>ModifyForwardSeventhBackendsPort</td>
<td>Modifies ports of CVMs bound to a Layer-7 listener.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/8992" target="_blank">DeregisterInstancesFromForwardLBFourthListener</a></td>
<td>DeregisterInstancesFromForwardLBFourthListener</td>
<td>Unbinds CVMs from the forwarding rules of a CLB Layer-4 listener.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/8991" target="_blank">DeregisterInstancesFromForwardLB</a></td>
<td>DeregisterInstancesFromForwardLB</td>
<td>Unbinds CVMs from the forwarding rules of a CLB Layer-7 listener.</td>
</tr>
</tbody></table>

### Health check APIs

<table>
<thead>
<tr>
<th width="30%">API Name</th>
<th width="40%">Action ID</th>
<th width="30%">Feature</th>
</tr>
</thead>
<tbody><tr>
<td>DescribeForwardLBHealthStatus</td>
<td>DescribeForwardLBHealthStatus</td>
<td>Queries the health check of a CLB instance.</td>
</tr>
</tbody></table>

### Redirection APIs
<table>
<thead>
<tr>
<th width="30%">API Name</th>
<th width="40%">Action ID</th>
<th width="30%">Feature</th>
</tr>
</thead>
<tbody><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/9016" target="_blank">DescribeRewrite</a></td>
<td>DescribeRewrite</td>
<td>Queries the redirection relationship of a CLB instance.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/9014" target="_blank">DeleteRewrite</a></td>
<td>DeleteRewrite</td>
<td>Deletes the redirection relationship of a CLB instance.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/9015" target="_blank">ManualRewrite</a></td>
<td>ManualRewrite</td>
<td>Adds the redirection relationship to a CLB instance manually.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214/9017" target="_blank">AutoRewrite</a></td>
<td>AutoRewrite</td>
<td>Generates the redirection relationship for a CLB instance automatically.</td>
</tr>
</tbody></table>
