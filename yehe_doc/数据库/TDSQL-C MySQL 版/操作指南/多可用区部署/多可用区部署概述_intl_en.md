The engine of TDSQL-C for MySQL allows deploying a cluster across AZs. A multi-AZ cluster has superior disaster recovery capabilities than a single-AZ cluster and can protect your database against database instance failures, AZ outages, and even IDC-level failures.

The multi-AZ deployment scheme of TDSQL-C for MySQL guarantees the high availability and failover capability of database instances by combining multiple AZs into a single "multi-AZ".

## Prerequisites
- The cluster region has at least two AZs.
- The target AZ has sufficient computing resources.
- Database version requirements:
 - Database version 5.7 with kernel minor version 2.0.15 or above.
 - Database version 8.0 with kernel minor version 3.0.1 or above.

## Multi-AZ Deployment Architecture
![](https://qcloudimg.tencent-cloud.cn/raw/aaff0742dbbd7eac1816da5cd329886d.png)

## Supported Regions and AZs
- Currently, this feature is in beta test and only supports the following regions and AZs.
- This feature will gradually support more regions and AZs.
- If required by your business, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for deployment in other regions and AZs.

<table class="table-striped">
<tbody>
<tr><th>Supported Region</th><th>Supported AZ</th></tr>
<tr>
<td rowspan="2">North China (Beijing)</td>
<td>Beijing Zone 5</td></tr>
<tr>
<td>Beijing Zone 7</td></tr>
<td rowspan="2">South China (Guangzhou)</td>
<td>Guangzhou Zone 4</td></tr>
<tr>
<td>Guangzhou Zone 6</td></tr>
<td rowspan="2">East China (Shanghai)</td>
<td>Shanghai Zone 2</td></tr>
<tr>
<td>Shanghai Zone 4</td></tr>
</tbody></table>

## How to Implement Multi-AZ Architecture
You can create a cluster in multi-AZ deployment mode in the TDSQL-C for MySQL console. Your existing single-AZ clusters will also be upgraded to the multi-AZ mode. The upgrade will be automatically completed through online data migration without affecting your business. For more information, see [Configuring Multi-AZ Deployment](https://intl.cloud.tencent.com/document/product/1098/44326).

## Multi-AZ Billing Description
There are no additional fees for the multi-AZ feature for the time being.
>?Currently, single-AZ clusters can also be upgraded to multi-AZ clusters for free.

## Multi-AZ Information Display
1. The **[cluster list](https://console.cloud.tencent.com/cynosdb)** page displays the information of the cluster's primary AZ and supports filtering.
![](https://qcloudimg.tencent-cloud.cn/raw/cbe735bac803637ab8272f7605fdd3fb.png)
2. On the cluster details page, you can view the AZs where data is distributed in **Basic Info** > **Availability Info**.
![](https://qcloudimg.tencent-cloud.cn/raw/30da2dc7fbaaf8970ece5f61032bd1d1.png)![](https://qcloudimg.tencent-cloud.cn/raw/44e89ae4ebaaaae910cabb4102529000.png)
