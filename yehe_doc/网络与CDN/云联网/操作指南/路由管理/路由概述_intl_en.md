After a CCN instance is created, the system will automatically create a route table and control route entries to manage traffic on CCN. You cannot add or delete routes, but you can enable or disable them.  

## Automatic Route Addition
To automatically add a CCN route, there are three stages:
1. Before addition: logic for receiving routes, i.e., determining which routes can be added to the CCN route table.
2. During addition: logic for route to take effect by default, i.e., determining which routes added to CCN can take effect.
3. After addition: logic for setting route priority, i.e., determining which effective routes will forward traffic.

### 1. Before addition
- The associated instance is a VPC: for a new subnet, the destination is a subnet IP range, and the next hop is VPC route to CCN.
- The associated instance is a direct connect gateway: the destination is an IDC IP range, and the next hop is direct connect gateway route to CCN. The route can be propagated in the following two ways:
 1. Custom: you need to manually enter the IDC IP range to propagate to CCN, and the next hop is the corresponding direct connect gateway, which facilitates IP range convergence and filtering.
 2. Auto-propagation: the route is dynamically learned through BGP, and the next hop is the corresponding direct connect gateway, which makes it easy to perceive route changes in IDC. Routes are published to CCN based on AS-PATH:
   - If the AS-PATH lengths are the same, CCN will accept all routes.
   - If the AS-PATH lengths are different, CCN will accept routes with a shorter AS-PATH.

>?
>- Auto-propagation is currently in beta. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9CVPC&step=1).
>- AS-PATH description:
>  - The information of AS-PATH can be viewed in the direct connect gateway.
>  - AS-PATH supports a 32-bit string. If the string is exceptional, the route will be deleted, and a string exception event will be reported, for which you can configure event alarms.
>  - The maximum AS-PATH length is 30; if the maximum length is exceeded, the AS-PATH will be truncated, and a truncation event will be reported, for which you can configure event alarms.
>  - The AS-PATH that passes through direct connect gateway - CCN - direct connect gateway now supports three new AS numbers (45090, 139341, and 45090).


### 2. During addition
- Check policy: if a new route overlaps any existing route, the new one will become invalid by default to avoid affecting existing routes. You can enable it after assessing the impact.
- Non-check policy: all routes will be valid except ECMP routes. For more information, please see the routing logic in [same IP ranges](#same) in the section 3 below.
>?The non-check policy is currently in beta. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9CVPC&step=1).


### 3. After addition
- Different IP ranges overlapped: the route with the longest mask will be used. A more specific IP range has a higher priority. For example, if the destination of route A is <code>10.0.1.0/20</code> and that of route B is <code>10.0.1.0/24</code>, route B will be first matched based on the longest mask principle when both routes are enabled.
<span id="same"></span>
- Same IP ranges: any route whose next hop is direct connect gateway supports ECMP. For example, you can enable multiple routes to the same IP range <code>10.0.1.0/20</code>. However, other routes do not support ECMP and cannot be enabled simultaneously. For example, if there are two or more routes to the IP range <code>10.0.1.0/20</code> whose next hops are VPC or VPC and direct connect gateway, only one route can be enabled.
>?See below for the description of inbound routes in the CCN-Direct Connect network architecture. For more information, see [Direct Connect Gateway Overview](https://intl.cloud.tencent.com/document/product/216/38746).
>- The CCN-based direct connect gateway created before September 15, 2020, 00:00:00 publishes the route of subnet CIDR block to the dedicated tunnel. For a BGP dedicated tunnel, the VPC subnet CIDR block is synced to IDC based on the BGP protocol.
>- The CCN-based direct connect gateway created after September 15, 2020, 00:00:00 publishes the route of VPC CIDR block to the dedicated tunnel. For a BGP dedicated tunnel, the VPC CIDR block is synced to IDC based on the BGP protocol.


## Automatic Route Deletion
<table>
<thead>
<tr>
<th>Next Hop Type</th>
<th>When the Route will be Deleted</th>
</tr>
</thead>
<tbody><tr>
<td>VPC in public cloud</td>
<td>VPC instance is unbound or subnet is deleted</td>
</tr>
<tr>
<td>Direct Connect Gateway</td>
<td>1. Direct Connect gateway is unbound<br>2. Route is modified in Direct Connect gateway<br>&nbsp;i. Manual entry (static): deletion<br>&nbsp;ii. Dynamic learning (BGP): opposite route update</td>
</tr>
</tbody>
</table>
