During the use of TencentDB for MySQL, you may encounter problems related to instance access, instance maintenance, database and table creation as well as data backup and rollback. This document describes common operations in TencentDB for MySQL instances and relevant products.
## Instance
A TencentDB for MySQL [instance](https://intl.cloud.tencent.com/document/product/236/5147) can contain multiple user-created databases and can be accessed using the same tools and applications as those for a standalone database instance. Below are common operations in TencentDB for MySQL instances, databases, and tables.

### Common Operations
- [Accessing an instance over the public network](http://intl.cloud.tencent.com/document/product/236/9038)

- Maintaining an instance
 - [Setting instance maintenance time](https://intl.cloud.tencent.com/document/product/236/10929)
 - [Specifying a project for an instance](http://intl.cloud.tencent.com/document/product/236/8460)

- Modifying an instance
 - [Upgrading database engine](http://intl.cloud.tencent.com/document/product/236/8126)
 - [Adjusting database instance specification](https://intl.cloud.tencent.com/document/product/236/19707)

- Scaling an instance
 - [Read-only instance](http://intl.cloud.tencent.com/document/product/236/7270)
 - [RO group of read-only instances](https://intl.cloud.tencent.com/document/product/236/11361)
 - [Managing a disaster recovery instance](https://intl.cloud.tencent.com/document/product/236/7272)

- [Terminating an instance](https://intl.cloud.tencent.com/document/product/236/31895)


### Database Management
- [Creating a database and table](http://intl.cloud.tencent.com/document/product/236/8465)
- [Manipulating instances in batches](https://intl.cloud.tencent.com/document/product/236/8466)
- [Deleting a database and table](https://intl.cloud.tencent.com/document/product/236/31905)

## Parameter Template
A [parameter template](http://intl.cloud.tencent.com/document/product/236/8461) is used to manage how the parameters of a database engine are configured. A database parameter set is just like a container of engine configuration values which can be applied to one or more database instances. Below are common operations currently supported by a TencentDB instance parameter template.

### Common Operations
- [Creating a parameter template](https://intl.cloud.tencent.com/document/product/236/31906#.E6.96.B0.E5.BB.BA.E5.8F.82.E6.95.B0.E6.A8.A1.E6.9D.BF)
- [Copying a parameter template](https://intl.cloud.tencent.com/document/product/236/31906#.E5.A4.8D.E5.88.B6.E5.8F.82.E6.95.B0.E6.A8.A1.E6.9D.BF)
- [Modifying a parameter template](https://intl.cloud.tencent.com/document/product/236/31906#.E4.BF.AE.E6.94.B9.E5.8F.82.E6.95.B0)
- [Importing a parameter template](https://intl.cloud.tencent.com/document/product/236/31906#.E5.AF.BC.E5.85.A5.E5.8F.82.E6.95.B0)

## Data
Common data operations in TencentDB for MySQL are as follows:

### Backup and Rollback

- [Downloading a backup file](http://intl.cloud.tencent.com/document/product/236/7274)
- [Restoring a database from a physical backup file](https://intl.cloud.tencent.com/document/product/236/31910)
- [Rolling data back](http://intl.cloud.tencent.com/document/product/236/7276)

### Data Import and Export

- [Importing data](https://intl.cloud.tencent.com/document/product/236/8463)
- [Migrating data offline](https://intl.cloud.tencent.com/document/product/236/8464)

## Security Group
A [TencentDB security group](https://intl.cloud.tencent.com/document/product/236/14470) is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB databases. Below are common operations for TencentDB security groups.

- [Creating a security group](https://intl.cloud.tencent.com/document/product/236/14470#.E5.88.9B.E5.BB.BA.E5.AE.89.E5.85.A8.E7.BB.84)
- [Configuring a security group for TencentDB](https://intl.cloud.tencent.com/document/product/236/14470#.E4.B8.BA.E4.BA.91.E6.95.B0.E6.8D.AE.E5.BA.93.E9.85.8D.E7.BD.AE.E5.AE.89.E5.85.A8.E7.BB.84)
- [Deleting a security group](https://intl.cloud.tencent.com/document/product/236/14470#.E5.88.A0.E9.99.A4.E5.AE.89.E5.85.A8.E7.BB.84)
- [Cloning a security group](https://intl.cloud.tencent.com/document/product/236/14470#.E5.85.8B.E9.9A.86.E5.AE.89.E5.85.A8.E7.BB.84)
- [Adding a rule to a security group](https://intl.cloud.tencent.com/document/product/236/14470#.E5.90.91.E5.AE.89.E5.85.A8.E7.BB.84.E4.B8.AD.E6.B7.BB.E5.8A.A0.E8.A7.84.E5.88.99)
- [Importing/exporting a security group rule](https://intl.cloud.tencent.com/document/product/236/14470#.E5.AF.BC.E5.85.A5.E5.AF.BC.E5.87.BA.E5.AE.89.E5.85.A8.E7.BB.84.E8.A7.84.E5.88.99)

