## Overview
PostgreSQL for Serverless (ServerlessDB) is a PostgreSQL-based database product that enables on-demand allocation of resources. It can automatically allocate resources according to the actual number of requests.

With a traditional database instance, you need to manually adjust the database specification and capacity according to the actual business usage, which not only takes up your time but also may cause resource waste due to the underuse of database resources.
With PostgreSQL for Serverless, you can create a database instance for easy use without caring about the instance specifications. You only need to pay for the actual usage when the database is active.

>?PostgreSQL for Serverless is currently in beta test free of charge. You can create an instance directly through the [CreateServerlessDBInstance](https://intl.cloud.tencent.com/document/product/409/38880) API.

## System Architecture
After users are connected to a database, requests will be forwarded uniformly through the PostgreSQL for Serverless proxy layer before data operations are performed. When the number of user requests increases, the database will automatically respond. Currently, up to 40,000 QPS is supported for one single user.
![](https://main.qcloudimg.com/raw/85f9c5aa5403f17f3d4d21f45690ce91.png)

## Features
### High availability
PostgreSQL for Serverless supports the architecture of one primary instance and one secondary instance for high availability. When the primary instance becomes unavailable due to an exception, the database will automatically start the secondary instance, to which business connections will be transferred so as to prevent business interruption.

### Automatic backup
PostgreSQL for Serverless automatically backs up the entire database at 1:00 AM every day and backs up database logs once every 15 minutes or when the number of log files reaches 60. All backups are retained for 7 days.
Backup is automatically performed on the backend. Currently, you cannot view, download, or restore data from backups.
