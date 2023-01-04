In scenarios with more reads but fewer writes, a single instance may not be able to handle the read load, which may even affect the business. To implement the auto-scaling of read capabilities and mitigate the pressure, you can create one or multiple read-only instances to sustain high numbers of database reads and increase the application throughput.

## Prerequisite
The compatible database version is MySQL 5.7 or 8.0 (kernel version 3.1.2 or later).

## Billing
- **Instance Specification Billing Mode**: The billing mode of the read-only instance is the same as that of the read-write instance. For example, if the read-write instance is monthly subscribed, so is the new read-only instance.
- **Storage Billing Mode**: As TDSQL-C for MySQL is billed by the actual storage used per hour, you don’t need to purchase storage space in advance. The storage of the read-only instance uses that of the entire cluster

## Features
- **Region and AZ**: Read-only instance needs to be deployed in the same AZ of a region where the read-write instance resides.
- **Database Compatibility**: It must be the same as that of the read-write instance.
- **Specification**: It may be different from that of the read-write instance and can be modified at any time. The read-only instance must have a specification not less than that of the read-write instance; otherwise, it may experience high latency and load.
- **Instance Name**: It must contain less than 60 letters, digits, or symbols (-_.).
- **Network**: It is the same as that of the read-write instance.
- **Project**: It is the same as that of the read-write instance.
- **Monitoring and Alarm**: It provides rich monitoring views of system performance indicators, such as memory utilization, QPS, TPS, and max connections.

## Feature Limits
- **Read-only instances can be created**: 15
- **Database management**: Databases can be neither created nor deleted.
- **Account management**: Account creation, deletion, authorization, password modification of the account are not supported.

## Creating Read-Only Instance
For more information, see [Creating Read-Only Instance](https://intl.cloud.tencent.com/document/product/1098/40631).
