
## Supported Services
The services supported by database audit are as follows:
- TencentDB for MySQL 5.6, 5.7, and 8.0 (two-node and three-node).
- TDSQL-C for MySQL.
- TencentDB for MongoDB 4.0.

## Audit Price
[Database Audit](https://console.cloud.tencent.com/dls/mysql) is billed by the amount of audit log storage for every clock-hour, and usage duration shorter than one hour will be calculated as one hour.

<table>
<thead><tr><th rowspan="2" width=30%>Region</th><th colspan = "2" >Price (USD/GB/Hour)</th></tr><th>Frequent Access Storage</th><th>Infrequent Access Storage</th></tr></thead>
<tbody>
<tr>
<td>China (including finance regions)</td>
<td>0.00147059</td><td>0.00018382</td></tr>
<tr>
<td>Other countries and regions</td>
<td>0.00220588</td><td>0.00220588</td></tr>        
</tbody></table>

>?Currently, only TencentDB for MySQL supports both frequent and infrequent access storage, while other database products only support frequent access storage.

## Purchase Methods
- [Enabling TencentDB for MySQL Audit](https://intl.cloud.tencent.com/document/product/1102/41311)
- [Enabling TDSQL-C for MySQL Audit](https://intl.cloud.tencent.com/document/product/1102/41312)
- [Enabling TencentDB for MongoDB Audit](https://intl.cloud.tencent.com/document/product/1102/47769)

## Release
- After database audit is enabled for a pay-as-you-go TencentDB instance, when you release the instance, its audit service will also be stopped, and the logs will be automatically deleted and cannot be recovered.
- After database audit is enabled for a monthly subscribed TencentDB instance, when you release the instance in advance or upon expiration, its audit service will also be stopped, and the logs will be automatically deleted and cannot be recovered.

## Overdue Payment Policy
1. **When your account balance becomes negative**:
   - You can continue to use the SQL audit service for two hours from the moment your account balance becomes negative. We will also continue to bill you for this period.
   - When your account has overdue payments for two hours, the SQL audit service will be **automatically stopped**, and billing will stop.

2. **After the service is automatically stopped**:
   - If you top up your account to a positive balance within 24 hours after the SQL audit service is automatically stopped, it will be resumed, and billing will continue; otherwise, it cannot be resumed.
   - If your account balance remains negative after 24 hours, the logs will be deleted and cannot be recovered.
