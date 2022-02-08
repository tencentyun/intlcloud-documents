
For applications with high requirements of service continuity, data reliability, and compliance, TencentDB for MySQL provides cross-AZ and cross-region disaster recovery solutions to help enhance your capability to deliver continued services at low costs and improve data reliability.

### Intra-region Disaster Recovery
You can create [two-node](https://intl.cloud.tencent.com/document/product/236/38328) and [three-node](https://intl.cloud.tencent.com/document/product/236/38328) TencentDB for MySQL instances to support multi-AZ deployment. Physical servers of a multi-AZ instance are deployed in different AZs in the same region. When an AZ fails, the business traffic will be switched to another AZ swiftly, which is imperceptible to the business and requires no changes at the application layer to achieve intra-region disaster recovery.
>?As the nodes of a multi-AZ instance are in different AZs, there may be an additional network sync delay of 2–3 ms.

For more information on intra-region disaster recovery, see [High Availability (Multiple AZs)](https://intl.cloud.tencent.com/document/product/236/8459).

### Cross-region Disaster Recovery
The intra-region disaster recovery capability of TencentDB for MySQL is limited to different AZs in the same region. To further improve the availability, TencentDB for MySQL also supports cross-region data disaster recovery.

You can asynchronously replicate data in a TencentDB for MySQL instance in region A to another instance (disaster recovery instance) in region B through DTS. The disaster recovery instance has an independent connection address, account, and permissions. If a major failure occurs in region A and cannot be fixed in a short time, you can perform failover whenever needed. Specifically, you can quickly forward application requests to the disaster recovery instance simply by modifying the database connection configuration in the application, thereby delivering a finance-grade database availability.

For more information on cross-region disaster recovery, see [Disaster Recovery Instance](https://intl.cloud.tencent.com/document/product/236/7272).

