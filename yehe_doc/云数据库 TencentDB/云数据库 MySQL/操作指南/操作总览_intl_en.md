During the use of TencentDB for MySQL, you may encounter problems related to instance access, instance maintenance, database and table creation as well as data backup and rollback. This document describes common operations in TencentDB for MySQL instances and relevant products.
## Instances
A TencentDB for MySQL [instance](https://intl.cloud.tencent.com/document/product/236/5147) can contain multiple user-created databases and can be accessed using the same tools and applications as those for a standalone database instance. Below are common operations in TencentDB for MySQL instances, databases, and tables.

### Common operations
- [Accessing MySQL Database](https://intl.cloud.tencent.com/document/product/236/3130)

- Maintaining an instance
 - [Setting Instance Maintenance Period](https://intl.cloud.tencent.com/document/product/236/10929)
 - [Specifying Project for Instance](https://intl.cloud.tencent.com/document/product/236/8460)

- Modifying an instance
 - [Upgrading Database Engine](https://intl.cloud.tencent.com/document/product/236/8126)
 - [Adjusting Database Instance Specification](https://intl.cloud.tencent.com/document/product/236/19707)

- Scaling an instance
 - [Read-Only Instance](https://intl.cloud.tencent.com/document/product/236/7270)
 - [RO Group of Read-only Instance](https://intl.cloud.tencent.com/document/product/236/11361)
 - [Disaster Recovery Instance](https://intl.cloud.tencent.com/document/product/236/7272)

- [Terminating Instance](https://intl.cloud.tencent.com/document/product/236/31895)

### Database management
- [Creating Database and Table](http://intl.cloud.tencent.com/document/product/236/8465)
- [Batch Operating Instance](https://intl.cloud.tencent.com/document/product/236/8466)
- [Dropping Database/Table](https://intl.cloud.tencent.com/document/product/236/31905)

## Parameter Template
A [parameter template](https://intl.cloud.tencent.com/zh/document/product/236) is used to manage how the parameters of a database engine are configured. A database parameter set is just like a container of engine configuration values which can be applied to one or more database instances. Below are common operations currently supported by a TencentDB instance parameter template.

## Data
Common data operations in TencentDB for MySQL are as follows:

### Backup and rollback
- [Restoring Database from Physical Backup](https://intl.cloud.tencent.com/document/product/236/31910)
- [Restoring Database from Logical Backup](https://intl.cloud.tencent.com/document/product/236/31909)
- [Database Rollback](https://intl.cloud.tencent.com/document/product/236/7276)

### Data import and export
- [Data Import](https://intl.cloud.tencent.com/document/product/236/8463)
- [Offline Migration of Data](https://intl.cloud.tencent.com/document/product/236/8464)

## Security Groups
A [TencentDB security group](https://intl.cloud.tencent.com/document/product/236/14470) is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB databases.
#### Common operations
- [Security Group Configuration for TencentDB](https://intl.cloud.tencent.com/document/product/236/14470#.E4.B8.BA.E4.BA.91.E6.95.B0.E6.8D.AE.E5.BA.93.E9.85.8D.E7.BD.AE.E5.AE.89.E5.85.A8.E7.BB.84)
- [Security Group Rule Import](https://intl.cloud.tencent.com/document/product/236/14470#.E5.AF.BC.E5.85.A5.E5.AE.89.E5.85.A8.E7.BB.84.E8.A7.84.E5.88.99)
- [Security Group Clone](https://intl.cloud.tencent.com/document/product/236/14470#.E5.85.8B.E9.9A.86.E5.AE.89.E5.85.A8.E7.BB.84)
- [Security Group Deletion](https://intl.cloud.tencent.com/document/product/236/14470#.E5.88.A0.E9.99.A4.E5.AE.89.E5.85.A8.E7.BB.84)

