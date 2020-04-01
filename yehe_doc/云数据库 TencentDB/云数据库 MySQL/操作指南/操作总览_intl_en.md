During the use of TencentDB for MySQL, you may encounter problems related to instance access, instance maintenance, database and table creation as well as data backup and rollback. This document describes common operations in TencentDB for MySQL instances and relevant products.
## Instance
A TencentDB for MySQL [instance](https://intl.cloud.tencent.com/document/product/236/5147) can contain multiple user-created databases and can be accessed using the same tools and applications as those for a standalone database instance. Below are common operations in TencentDB for MySQL instances, databases, and tables.

### Common operations
- [Accessing MySQL Instance](https://intl.cloud.tencent.com/document/product/236/3130)

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
- [Creating a database and table](https://intl.cloud.tencent.com/document/product/236/8465)
- [Manipulating instances in batches](https://intl.cloud.tencent.com/document/product/236/8466)
- [Dropping a database and table](https://intl.cloud.tencent.com/document/product/236/31905)

## Parameter Template
A [parameter template](https://intl.cloud.tencent.com/document/product/236/8461) is used to manage how the parameters of a database engine are configured. A database parameter set is just like a container of engine configuration values which can be applied to one or more database instances. Below are common operations currently supported by a TencentDB instance parameter template.
#### Common operations
- [Creating a Parameter Template](https://intl.cloud.tencent.com/document/product/236/31906#.E6.96.B0.E5.BB.BA.E5.8F.82.E6.95.B0.E6.A8.A1.E6.9D.BF)
- [Copying a Parameter Template](https://intl.cloud.tencent.com/document/product/236/31906#.E5.A4.8D.E5.88.B6.E5.8F.82.E6.95.B0.E6.A8.A1.E6.9D.BF)
- [Modifying a Parameter Template](https://intl.cloud.tencent.com/document/product/236/31906#.E4.BF.AE.E6.94.B9.E5.8F.82.E6.95.B0)
- [Importing Parameters](https://intl.cloud.tencent.com/document/product/236/31906#.E5.AF.BC.E5.85.A5.E5.8F.82.E6.95.B0)

## Data
Common data operations in TencentDB for MySQL are as follows:

### Backup and rollback
- [Restoring Database from Physical Backup](https://intl.cloud.tencent.com/document/product/236/31910)
- [Restoring Database from Physical Backup File](https://intl.cloud.tencent.com/document/product/236/31909)
- [Database Rollback](https://intl.cloud.tencent.com/document/product/236/7276)

### Data import and export
- [Data Import](https://intl.cloud.tencent.com/document/product/236/8463)
- [Migrating data offline](https://intl.cloud.tencent.com/document/product/236/8464)

## Security Group
A [TencentDB security group](https://intl.cloud.tencent.com/document/product/236/14470) is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB databases. Below are common operations for TencentDB security groups.

