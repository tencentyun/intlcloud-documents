After a CCN instance is created, the system will automatically create a route table and control route entries to manage traffic on CCN. You cannot manually add or delete routes, but you can enable or disable them.

## Automatic Route Addition
The logic of automatic route addition in CCN involves three stages as shown below:
1. Before addition: logic for receiving routes, i.e., determining which routes can be added to the CCN route table.
2. During addition: logic for default route application. This determines which routes added to CCN can take effect.
3. After addition: logic for setting route priority, i.e., determining which effective routes will forward traffic.

### 1. Before addition
- The associated instance is a VPC in the public cloud: for a new subnet, the destination is a subnet IP range, and the next hop is VPC route to CCN.
- The associated instance is a Direct Connect gateway: the destination is an IDC IP range, and the next hop is Direct Connect gateway route to CCN. There are two ways to pass the route:
 1. Manual entry (static): you need to manually enter the IDC IP range to be passed to CCN, and the next hop is the corresponding Direct Connect gateway, which facilitates IP range convergence and filtering.
 2. Dynamic learning (BGP): this refers to dynamically learning about routes through BGP, and the next hop is the corresponding Direct Connect gateway, which makes it easy to perceive routing changes in IDC. Currently, routes published to CCN can be controlled based on AS-PATH:
   - If the AS-PATH lengths are the same, CCN will accept all routes.
   - If the AS-PATH lengths are different, CCN will accept routes with a shorter AS-PATH.

>?
>- Dynamic learning (BGP) is in beta testing. If you want to use it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9CVPC&step=1) for application.
>- AS-PATH description:
>  1. The information of AS-PATH can be viewed in the Direct Connect gateway.
>  2. 32-bit string is supported. If the string is exceptional, the route will be deleted, and a string exception event will be reported, for which you can configure event alarming.
>  3. The maximum AS-PATH length is 30; if the maximum length is exceeded, the AS-PATH will be truncated, and a truncation event will be reported, for which you can configure event alarming.
>  4. Three AS numbers (45090, 139341, and 45090) will be added to the AS-PATH that passes through Direct Connect gateway - CCN - Direct Connect gateway.

### 2. During addition
- Check policy: if it overlaps any existing route, routes newly added will become invalid by default to avoid affecting existing routes. You can adjust their validity after assessing the impact.
- No-check policy: all routes will be valid except ECMP routes. For more information, please see the routing logic in [same IP ranges](#same) in section 3 below.
>? The no-check policy feature is in beta testing. If you want to use it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9CVPC&step=1) to apply.

### 3. After addition
- Different IP ranges overlapped: the longest mask matching principle is applied, which gives higher priority to more specific IP ranges. For example, if the destination IP range of route A is <code>10.0.1.0/20</code> and the destination IP range of route B is <code>10.0.1.0/24</code>, route B will be first matched based on the longest mask matching principle when both routes A and B are enabled.
<span id="same"></span>
- Same IP ranges: routes whose next hops are direct connect gateways support ECMP. For example, you can enable multiple routes whose destination IP ranges are <code>10.0.1.0/20</code>. Other routes do not support ECMP. This means that these routes cannot be enabled simultaneously. For example, if there are two or more routes whose destination IP ranges are <code>10.0.1.0/20</code> and whose next hops are VPC or VPC and direct connect gateway, only one route can be enabled.
>?See the following notes for the inbound route of the connection network architecture in CCN. More information can be viewed in Direct Connect Gateway Overview.
>- The CCN direct connect gateway created before September 15, 2020, 00:00:00 publishes the route of subnet CIDR block to the dedicated tunnel. For a BGP dedicated tunnel, the VPC subnet CIDR block is synced to IDC based on the BGP protocol.
>- The CCN direct connect gateway created after September 15, 2020, 00:00:00 publishes the route of VPC CIDR block to the dedicated tunnel. For a BGP dedicated tunnel, the VPC CIDR block is synced to IDC based on the BGP protocol..

## Automatic Route Deletion
<table>
<thead>
<tr>
<th>Next Hop Type</th>
<th>Trigger of Route Deletion</th>
</tr>
</thead>
<tbody><tr>
<td>VPC in public cloud</td>
<td>VPC instance is unbound or subnet is deleted</td>
</tr>
<tr>
<td>Direct Connect gateway</td>
<td>1. Direct Connect gateway is unbound<br>2. Route is modified in Direct Connect gateway<br>&nbsp;i. Manual entry (static): deletion<br>&nbsp;ii. Dynamic learning (BGP): opposite route update</td>
</tr>
</tbody></table>
