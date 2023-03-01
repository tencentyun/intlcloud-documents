This document describes the common concepts of TDSQL-C for MySQL to help you better understand and use it.

## Concepts
- **Tencent Cloud console**: Web-based UIs.

- **Region**: A physical IDC. In general, a TDSQL-C for MySQL instance and a CVM instance should be in the same region to achieve the best access performance.
- **Availability zone (AZ)**: A physical location with independent power supply and network resources within a region. There are no substantial differences between different AZs in the same region.
- **Multi-AZ**: A physical location created by combining multiple AZs in the same region.
- **Read-write instance**: A TDSQL-C for MySQL database resource in Tencent Cloud. A cluster can have only one read-write instance.
- **Read-only instance**: A compute node that can only be read from. A cluster can have 0–15 read-only instances.
- **Billing mode**: The billing mode of an instance resource, which can be monthly subscription, pay-as-you-go, or serverless.
- **Pay-as-you-go**: A postpaid billing mode, where you can apply for resources for on-demand use and will be charged based on the actual usage upon settlement.
- **Monthly subscription**: A prepaid billing mode, where you need to pay the fees for one or multiple months or even years based on your need for cloud resources.
- **Serverless**: TDSQL-C for MySQL Serverless adopts Tencent Cloud's proprietary serverless architecture for next-gen cloud-native relational database services. It is billed based on the actual computing and storage resource usage, so you only need to pay for what you use.
- **Instance type**: General or dedicated.
- **Compatible database version**: MySQL 5.7 and 8.0 currently.
- **Instance specification**: The specification configuration of a compute instance, such as 2-core 16 GB MEM.
- **Project**: Used to categorize and manage instance resources.
- **Tag**: A cloud resource management tool that allows you to use different standards to categorize, search for, and aggregate cloud resources with the same attributes.
- **Maintenance time**: To ensure the stability of your TencentDB instance, the backend system performs maintenance operations on the instance during the maintenance window from time to time. We highly recommend you set an acceptable maintenance time for your business instance, usually during off-peak hours, so as to minimize the potential impact on your business.
- **Security group**: Security access control to instances by specifying IP, protocol, and port rules for instance access.
- **Network**: A network made up of several nodes and linkages that connect them. It represents many objects and their interconnections. For performance and security considerations, only VPC network is supported currently.
- **Private read-write address**: The IP and port assigned to a database for both read and write requests within your VPC network.
- **Private read-only address**: The IP and port assigned to a database for read requests only within your VPC network.
- **Public read-write address**: The IP and port that provide public network access and support both read and write requests.
- **Public read-only address**: The IP and port that provide public network access and support read requests only.
- **Port**: A port in a computer, switch, or router.
- **Database**: A set of organized, shared, and centrally managed data that is stored on a computer for a long period.
- **Database account**: A username used to log in to and manage a database.
- **Character set**: A mapping relationship or encoding rule, including a coded character set and character encoding. The code points corresponding to a character set are mapped into binary sequences, so that they can be stored and processed by a computer.
- **Cloud Virtual Machine (CVM)**: A scalable computing service provided by Tencent Cloud.
- **Monitoring**: To make it easier for you to view and stay up to date with instance conditions, TDSQL-C for MySQL provides a wide variety of performance monitoring metrics and convenient monitoring features (such as custom view, time comparison, and merged monitoring metrics).
- **Alarm policy**: You can create alarms to stay informed of the status changes of certain metrics. The specific metrics will be monitored for a certain period of time, and alarm notifications will be sent by SMS, email, and phone at specified intervals based on the given threshold.
- **Recycle bin**: A place where terminated instances are stored before elimination. Such instances can be restored.
- **Backup**: Data is stored separately or as a file copy to tackle possible unexpected situations such as file or data loss or corruption.
- **Automatic backup**: Currently, snapshot backup is supported. You can set the backup time for the system to automatically save data.
- **Manual backup**: You can manually create backup files at any time. Manual backup is supported only for full backup.
- **Database audit**: It can record accesses to databases and executions of SQL statements to help you manage risks and improve the database security.
