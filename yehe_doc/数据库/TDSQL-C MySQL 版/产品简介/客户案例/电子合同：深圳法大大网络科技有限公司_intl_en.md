TDSQL-C for MySQL adopts a storage-computing separation architecture to enable fast configuration upgrade/downgrade, swift failover, and global data consistency. It delivers high stability, reliability, performance, and scalability like commercial databases while featuring simplicity, openness, and efficient iteration like open-source cloud databases.

This document describes how TDSQL-C for MySQL helps Shenzhen Fadada Network Technology Co., Ltd. tackle business challenges.

## Company Overview
Fadada is a leading cloud-based electronic signature and contract platform in China. It is committed to providing enterprises, governments, and individuals with signing and management services of electronic contracts and documents based on legal digital signature technologies. Its major products and services include contract template, contract editing, smart review, contract signing, and evidence storage and provision. In addition, it integrates and offers online judicial authentication and attorney services to close the online loop of the entire contract lifecycle.
Industry: Electronic contract platform

## Project Requirements
About 50 million contracts were added every month, and the database needed to be manually sharded once every three months on average, which increased the labor and time costs. There were 800 million historical contracts, which has to be retrieved from multiple databases in sequence during contract search, so the average search time was about 10 seconds, which directly compromised the business efficiency.

## Solution
Based on the architecture of storage-computing separation, TDSQL-C for MySQL can well sustain the storage and efficient query of massive amounts of data. It securely stores the customer's more than 800 million electronic contracts, breaking through the capacity bottleneck of the primary business database and eliminating the need of manual sharding. With multiple read-only nodes added, data of such historical contracts can be searched within just 0.2 seconds, getting rid of slow queries.
![](https://qcloudimg.tencent-cloud.cn/raw/8298168ab2abd93a71a7e342e0d3c59b.png)

## Benefits to Customer
TDSQL-C for MySQL is 100% compatible with MySQL 5.7 and 8.0 features, so there is no need to make basic transformations during application migration to archive high volumes of historical data and query the data in real time. Its elastic and massive storage capacity solves the problem of insufficient storage space in traditional MySQL databases. In addition, it adopts a read-write separation architecture and supports concurrent access to multiple application servers, which reduce the average query time from 10 to 0.2 seconds and greatly improve the query business experience.
