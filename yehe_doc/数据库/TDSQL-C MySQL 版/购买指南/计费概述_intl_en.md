This document describes all the billable items of TDSQL-C for MySQL.

## Billable items

| Billable Item | Description | Charge Applicable | Supported Billing Mode |
|---------|---------|---------|---------|
| Compute node | <li>Compute nodes include read-write nodes and read-only nodes.<li>Such fees are subject to the node region, specification, and usage duration. | Charged upon purchase/use | <li>Monthly subscription<li>Pay-as-you-go<li>Serverless |
| Storage space | <li>Storage space refers to the space used by data files, index files, log files (redo logs, undo logs, slow logs, and error logs), and temporary files. Fees are charged for the used storage space.<li>Such fees are subject to the data volume and storage duration. <dx-alert infotype="notice" title="">
Data files are stored in three copies for strong data consistency and reliability, and fees are charged based on the data volume in only one copy.
</dx-alert>| Charged upon purchase/use | <li>Monthly subscription <li>Pay-as-you-go |
| Backup storage space | <li>Backup files take up the storage space. Backup modes include automatic and manual, and backup objects include binlog and data. Storage space used by all backup files incurs fees under this billable item.<li>Such fees are subject to the capacity and retention duration. | Free of charge for now | Pay-as-you-go |
| Database audit | <li>TDSQL-C for MySQL provides database audit capabilities, which can record accesses to databases and executions of SQL statements to help you manage risks and improve the database security.<li>You need to pay for database audit only after it is enabled.</li>| Charged upon purchase/use | Pay-as-you-go |

## Supported billing modes

| Billing Mode                             | Supported Engine          | Payment Mode                       | Use Case                              |
| -------------------------------- | ----------------- | -------------------------------- | --------------------------------------------- |
| Monthly subscription                                                     | MySQL | [Prepaid](https://intl.cloud.tencent.com/document/product/555/42701). You need to pay the fees when creating an instance. | It is more cost-effective in the long term for businesses with stable needs than pay-as-you-go billing. Moreover, the longer a service is purchased, the less it costs. |
| Pay-as-you-go                                                     | MySQL | [Postpaid](https://intl.cloud.tencent.com/document/product/555/30328). You can apply for resources for on-demand use and will be charged based on the actual usage of resources upon settlement. | It is suitable for businesses that may fluctuate greatly and instantaneously. In this mode, instances can be released immediately after use to save costs. |
| Serverless | MySQL             | [Postpaid](https://intl.cloud.tencent.com/document/product/555/30328). You can set the maximum and minimum computing power values as needed first, but you will be charged based on the actual usage of computing and storage resources upon settlement. | It is suitable for business scenarios with low frequency and uncertain load such as development and testing. <dx-alert infotype="explain" title="Note">A serverless instance will start with the minimum CPU specification during initialization and will be downgraded if there are no requests in ten minutes after startup. Therefore, even if you don't use the instance after purchasing it, compute node fees will be charged for ten minutes.</dx-alert> |

