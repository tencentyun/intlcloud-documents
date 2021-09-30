## July 2021
<table>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
<tr>
<td>Optimize the UI design of CCN-based direct connect gateway publishing IDC IP ranges</td>
<td><ul><li>The visual configuration of publishing IDC IP ranges to CCN makes it easier and faster to interconnect IDC and CCN. </li><li>The connection status of CCN, direct connect gateway, and dedicated tunnels are displayed in real time (connected in green, and pending connection in gray).</li><li>The IP range description facilitates management.</li></ul></td>
<td>2021-07-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/216/39083">Publishing IDC IP Ranges to CCN</a></td>
</tr>
</table>


## April 2021
<table>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
<tr>
<td>Support modifying the connection bandwidth</td>
<td>The connection bandwidth can be modified in the console. The bandwidth value should be at least the total bandwidth caps of all dedicated tunnels (or 1 Mbps if there is no dedicated tunnel), and cannot exceed the port bandwidth.</td>
<td>2021-04-08</td>
<td><a href="https://tcloud-doc.isd.com/document/product/216/48587#xgzxdk">Managing Connections</a></td>
</tr>
</table>



## February 2021
<table>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
<tr>
<td>Upgrade dedicated tunnels</td>
<td>The dedicated tunnels are upgraded to versions 1.0 and 2.0, which change with the associated connection.<ul><li>The tunnel 1.0 now supports adjusting bandwidth.</li><li>The tunnel 2.0 supports features including bandwidth adjustment, health check, and network probe.</li></ul></td>
<td>2021-02-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/216/19250">Creating a Dedicated Tunnel</td>
</tr>
</table>

## January 2021
<table>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
<tr>
<td>Support viewing the route table of a CCN-based direct connect gateway</td>
<td>If you use a CCN-based direct connect gateway in the Direct Connect network architecture, you can view the IDC routes and CCN routes to the direct connect gateway in the console.</td>
<td>2021-01-20</td>
<td><a href="https://cloud.tencent.com/document/product/216/52093">Viewing Route Tables</a> </td>
</tr>
<tr>
<td>Support resource-level permissions for dedicated tunnel and direct connect gateway</td>
<td>Dedicated tunnel and direct connect gateway support resource-level permissions. You can use the CAM service to control access to your services, prevent data leakage and avoid security risks.</td>
<td>2021-01-19</td>
<td><a href="https://intl.cloud.tencent.com/document/product/216/39511">Cloud Access Management - Overview</a></td>
</tr>
</table>

## November 2020
<table>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
<tr>
<td>Update the port fees of the connection</td>
<td>Starting from February 1, 2021, all the new connections will be exempted from the initial installation fee.</td>
<td>2020-11-18</td>
<td><a href="https://intl.cloud.tencent.com/document/product/216/543">Billing Overview</a></td>
</tr>
<tr>
<td>Update the direct connect gateway charges</td>
<td>Starting from December 1, 2020, direct connect gateways will be charged with traffic fees. The inbound traffic is free of charge, while the outbound traffic fee is billed at a rate of 0.0015 USD/GB after a Tencent Cloud account uses up the free tier of 50 TB.</td>
<td>2020-11-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/216/543">Billing Overview</a></td>
</tr>
<tr>
<td>Update the route propagation of a CCN-based direct connect gateway</td>
<td>For a CCN-based direct connect gateway created after September 15, 2020:<ul><li>If a static dedicated tunnel is used, the IDC route to Tencent Cloud VPC should be configured in the local router.</li><li>If a BGP dedicated tunnel is used, the IDC will automatically obtain the VPC CIDR block based on the BGP protocol.</li></ul></td>
<td>2020-11-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/216/38746">Direct Connect Gateway Overview</td>
</tr>
<tr>
<td>Provide default alarm policies for connection and dedicated tunnel</td>
<td>After a connection is constructed, Tencent Cloud automatically configures a metric alarm for its bandwidth utilization. After a dedicated tunnel is created, its event alarms will be automatically configured.</td>
<td>2020-11-02</td>
<td><a href="https://intl.cloud.tencent.com/document/product/216/19244">Applying for Connection</a></td>
</tr>
</table>

## October 2020
<table>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
<tr>
<td>Add monitoring metrics</td>
<td>The DC connection now supports two more monitoring metrics: packet loss and packet error. The direct connect gateway now supports two more monitoring metrics: outbound traffic and inbound traffic.</td>
<td>2020-10-22</td>
<td><a href="https://intl.cloud.tencent.com/document/product/216/38401">Viewing Monitoring Data</a></td>
</tr>
</table>


## June 2020
<table>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
<tr>
<td>Update the compliance requirements of Direct Connect</td>
<td><ul><li>The Tencent Cloud Direct Connect Service Level Agreement is released.</li><li>The shared connection feature of new dedicated tunnels has stopped accepting new applications through the console and the API since August 1, 2020. The shared connection in use will not be affected.</li></ul></td>
<td>2020-06-29</td>
<td><a href="https://intl.cloud.tencent.com/document/product/216/37071">Notice on Changing the Direct Connect Features</td>
</tr>
</table>

## March 2020
<table>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
<tr>
<td>Integrate with the Cloud Monitor platform</td>
<td>The Cloud Monitor platform monitors connection and dedicated tunnel steadily and reliably, and provides alarms, helping you stay on top of your instances.</td>
<td>2020-03-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/216/38402">Configuring Alarm Policies</a></td>
</tr>
</table>

## July 2019
<table>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
<tr>
<td>Support the monthly billing cycle of ports</td>
<td>After paying for an initial installation fee, you can use the dedicated access port resources with a monthly rental fee.</td>
<td>2020-03-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/216/543">Billing Overview</a></td>
</tr>
</table>
