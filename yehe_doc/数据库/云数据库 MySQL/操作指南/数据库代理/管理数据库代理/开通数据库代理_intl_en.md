This document describes how to enable database proxy in the TencentDB for MySQL console.

Database proxy is a network proxy service between the TencentDB service and the application service. It is used to proxy all requests when the application service accesses the database. It provides advanced features such as automatic read/write separation, transaction split, connection pool, and connection persistence and boasts high availability, high performance, Ops support, and ease of use.

## Prerequisite
- The instance is running onthe two-node or three-node architecture.

## Note
- Database proxy currently is supported in the following regions:
  - Beijing (except Zones 1, 2, and 4), Shanghai (except Zone 1), Guangzhou (except Zones 1 and 2), Shanghai Finance (except Zones 1 and 2), Beijing Finance, Chengdu, Chongqing, Nanjing, and Hong Kong (China) (except Zone 1).
  - Tokyo (except Zone 1), Bangkok (except Zone 1), Virginia (except Zone 1), Silicon Valley (except Zone 1), Mumbai (except Zone 1), Seoul (except Zone 1), and Singapore (except Zones 1 and 2).
- Database proxy currently is supported on the following versions: two-node and three-node MySQL 5.7 (with kernel minor version 20211030 or later) and three-node MySQL 8.0 (with kernel minor version 20211202 or later). If you upgrade the kernel minor version of the source instance, the associated read-only and disaster recovery instances will be upgraded at the same time. For more information, see [Upgrading Kernel Minor Version](https://intl.cloud.tencent.com/document/product/236/36816).

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, select the source instance for which to enable database proxy and click its ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select the **Database Proxy** tab and click **Enable Now**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/vMSm892_10.png)
3. In the pop-up window, configure the following items and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ZUjv978_11.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Network</td>
<td>Select the network of the database proxy, which can only be a VPC.</td></tr>
<tr>
<td>Proxy Specification</td>
<td>Select 2-core 4000 MB memory, 4-core 8000 MB memory, or 8-core 16000 MB memory.</td></tr>
<tr>
<td>AZ and Node Quantity</td>
<td>1. Select the database proxy AZ. You can click <strong>Add AZ</strong> to add more AZs. The number of selectable AZs depends on how many AZs are available in the current region. You can select up to three AZs. <br>2. Select the node quantity. We recommend you set the quantity to 1/8 (rounded up) of the total number of CPU cores on the source and read-only instances; for example, if the source instance has 4 CPU cores, and the read-only instance has 8 CPU cores, then the recommended node quantity will be (4 + 8) / 8 ≈ 2. <blockquote class="rno-document-tips rno-document-tips-notice">    <div class="rno-document-tips-body">        <i class="rno-document-tip-icon"></i>        <div class="rno-document-tip-title">Notes</div>        <div class="rno-document-tip-desc"><ol><li>If the selected database proxy is not in the same AZ as the source instance, the write performance may drop when you connect to the database through the proxy. </li><li>If the calculated number of proxy nodes required exceeds the purchase limit, we recommend that you choose a higher proxy specification.</li></ol></div>    </div></blockquote></td></tr>
<tr>
<td>Security group</td>
<td>The security group of the source instance is selected by default. You can also select another existing security group or create a new one as needed. <blockquote class="rno-document-tips rno-document-tips-notice">    <div class="rno-document-tips-body">        <i class="rno-document-tip-icon"></i>        <div class="rno-document-tip-title">Note</div>        <div class="rno-document-tip-desc"><p>To access through the database proxy, you need to configure security group policies and open the private port (3306). For more information, see <a href="https://www.tencentcloud.com/document/product/236/14470">TencentDB Security Group Management</a>.</p></div>    </div></blockquote></td></tr>
<tr>
<td>Remarks</td>
<td>(Optional) Enter the remarks of the database proxy service to be enabled.</td></tr>
</tbody></table>
4. After successfully enabling the service, you can manage proxy nodes and view their basic information on the database proxy page. You can also modify the access address, network type, and remarks of the database proxy, view and adjust the connection configuration, and perform rebalance in the **Connection Address** section.
>?
>- You can view **Connections** in the proxy node list or view the performance monitoring data of each proxy node to check whether the numbers of connections on the nodes are unbalanced, and if so, you can distribute the connections by clicking **Rebalance**.
>- Rebalance will cause proxy nodes to restart, and the service will become unavailable momentarily during the restart. We recommend that you restart the service during off-peak hours. Make sure that your business has a reconnection mechanism.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/CH3a932_12.png)

