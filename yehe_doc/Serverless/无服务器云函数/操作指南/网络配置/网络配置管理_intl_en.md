## Overview
By default, a newly created cloud function has only the public network access permission. That is, when the cloud function is being executed, it can only access public network resources such as Tencent Cloud.

SCF supports the following network configurations:
<table>
<tr>
<th style="width:30%">Configuration Item</th>
<th>Description</th>
</tr>
<tr>
<td>Only public network access is enabled.</td>
<td>-</td>
</tr>
<tr>
<td>Public network access with a fixed public outbound IP is enabled.</td>
<td>The cloud function can access public network resources using a fixed IP address.</td>
</tr>
<tr>
<td>Only private network access is enabled.</td>
<td>The cloud function can access resources configured with the private network, such as databases and Redis.</td>
</tr>
<tr>
<td>Both public and private network accesses are enabled.</td>
<td>The cloud function can access public network resources and resources configured with the private network, such as databases and Redis.</td>
</tr>
<tr>
<td>Private network access and public network access with a fixed public outbound IP are enabled.</td>
<td>The cloud function can access public network resources using a fixed IP address and access resources configured with the private network, such as databases and Redis.</td>
</tr>
</table>

>?For more information about how the cloud function obtains the fixed public outbound IP, please see [Fixed Public Outbound IP](https://intl.cloud.tencent.com/document/product/583/38106).

## Prerequisites
- You have registered a Tencent Cloud account. If you have not, please go to the [Sign up](https://intl.cloud.tencent.com/register) page.
- You have [created a cloud function](https://intl.cloud.tencent.com/document/product/583/32742). 


## Procedure
### Performing network configuration
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index) and click **Function Service** in the left sidebar.
2. Choose a region at the top of the page and click the function to be configured.
3. In the **Function configuration** module, click **Edit** in the upper right corner.
4. Configure the network as needed by referring to the related [network configuration documentation](https://intl.cloud.tencent.com/document/product/583/38377).


### Viewing network configuration
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index) and click **Function Service** in the left sidebar.
2. Choose the region at the top of the page and click the function. The network configuration is displayed in the **Function configuration** module.




## Network Restrictions

### Concurrent connection count limits

Currently, a maximum of 60,000 connections can access the same ip:port concurrently. For non-persistent connections, since the release of intermediate devices takes time, the number of supported concurrent connections is smaller.

If multiple functions (or multiple requests of a function) need to access the same ip:port concurrently, you should pay attention to this limit. You can take the following measures to avoid using up the connections and making code errors.

- Use persistent connections as much as possible. During function initialization, complete and continuously reuse the connections. This avoids frequent connections and releases caused by the use of non-persistent connections during invocation. This measure gives full play to the supported connection count, but it is still limited by the connection count limit.
- Provide multiple ip:port pairs. In this way, connections are spread to multiple ip:port pairs to avoid reaching the connection count limit.

### Private network bandwidth limits

If the VPC is connected to a private network, the bandwidth for a single VPC is limited to 100 MB. The bandwidth is shared by the functions as well as the concurrent instances of these functions configured with the same VPC. To increase the private network bandwidth, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).


