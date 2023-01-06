This document describes the pricing of TDSQL-C for MySQL audit.

You need to pay for database audit only after it is enabled. For details, see [Enabling Audit in TDSQL-C for MySQL] (https://intl.cloud.tencent.com/document/product/1098/44614)
Database audit is billed by the stored log size for every clock-hour, and usage duration shorter than one hour will be calculated as one hour.

<table>
<thead><tr><th rowspan="2" width=30%>Region</th><th colspan = "2" >Price (USD/GB/Hour)</th></tr><th>Frequent Access Storage</th><th>Infrequent Access Storage</th></tr></thead>
<tbody>
<tr>
<td>China (including finance regions)</td>
<td>0.00147059</td><td>0.00018382</td></tr>
<tr>
<td>Other countries and regions</td>
<td>0.00220588</td><td>0.00027573</td></tr>        
</tbody></table>


## Frequent/Infrequent Access Storage
Frequent access storage represents an ultra-high-performance storage media with the best query performance. You can set the storage period, during which the audit data will be stored in the frequent access storage, but the data exceeding the period will be automatically transitioned to infrequent access storage. Different storages support the same audit capabilities with different performances.

You can set and modify the time period for frequent/infrequent access storage as needed, and the system will automatically move data between the frequent and infrequent access storage tiers based on the period, thus reducing your storage costs.


### Frequent/Infrequent storage architecture
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QTEv890_tapd_20397132_base64_1670577775_72.png)
As shown in the picture, If the data of the last 7 days is set to be stored in frequent access storage, older data will be automatically transitioned to infrequent access storage. After the frequent access storage period is extended, the audit data that falls in the period will be automatically migrated from infrequent access storage to frequent access storage.

### Performance differences between frequent and infrequent access storage

| Frequent access storage throughput | Infrequent access storage throughput |
| :-------------- | :------------- |
| 110,000 SQL statements/per second | 25,000 SQL statements/per second |

## Release
- After database audit is enabled for a pay-as-you-go/monthly subscribed TDSQL-C for MySQL instance, when you release an instance or an instance is released upon expiration, its corresponding audit service will also be stopped, and the logs will be automatically deleted and cannot be recovered.

## Overdue Payments
1. When your account balance becomes negative:
 - You can continue to use your database audit for 2 hours from the moment your account becomes negative. We will also continue to bill you for this period.
 - When your account has overdue payments for two hours, the database audit  service will be automatically stopped, and the billing will stop.

2. After the service is automatically stopped:
 - If you top up your account to a positive balance within 24 hours after the database audit is automatically stopped, it will be resumed, and the billing will continue; otherwise, it cannot be resumed.
 - If your account balance remains negative after 24 hours, the logs will be deleted and cannot be recovered.





