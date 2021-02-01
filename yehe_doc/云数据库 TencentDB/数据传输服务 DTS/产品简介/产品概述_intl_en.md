## Overview
Data Transmission Service (DTS) is a data transfer service that integrates such features as data migration, sync, and subscription, helping you migrate your databases without interrupting your business and build a high-availability database architecture for remote disaster recovery through real-time sync channels. Its data subscription feature grants you real-time access to incrementally updated data in your TencentDB instance, so that you can consume such data based on your business needs.
DTS is designed to take over complicated data interaction tasks, so that you can focus on upper-layer business development.


## Features
- **Data migration**
DTS helps you migrate databases of different types in different environments. It supports migrating self-built databases with public IP or connected to Tencent Cloud via VPN or Direct Connect and CVM-created databases to TencentDB instances. In addition, it allows you to check the status of all migration tasks and perform batch operations on multiple tasks.
With its data migration feature, DTS is your best choice for migrating data to the cloud. To migrate your data to Tencent Cloud, it only takes a few steps in DTS to set up data migration with no complicated configuration required. The migration process will not interrupt the service provided by your source database, thereby minimizing the impact of cloudification on your business.
- **Data sync**
DTS offers a data sync feature that enables real-time data sync between two TencentDB instances, making it suitable for application scenarios such as remote disaster recovery. Currently, this feature is supported only for TencentDB for MySQL instances.
- **Data subscription**
DTS gives you real-time access to incrementally updated data in your TencentDB instance, so that you can consume such data based on your business needs in various business scenarios, such as the implementation of cache update policy, async decoupling of business logics, real-time heterogeneous data sync, and real-time ETL data sync. Moreover, it allows you to dynamically add/delete subscribed objects, view subscribed data online, and modify consumption time point.
