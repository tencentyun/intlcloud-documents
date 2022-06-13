TDSQL-C for MySQL adopts a storage-computing separation architecture to enable fast configuration upgrade/downgrade and guarantee the global data consistency while being fully compatible with MySQL. It delivers high stability, reliability, performance, and scalability like commercial databases while featuring simplicity, openness, and efficient iteration like open-source cloud databases.

This document describes how TDSQL-C for MySQL helps Jiangsu Wisedu System Co., Ltd. tackle business challenges.

## Company Overview
To solve the difficulties and problems in daily student management, Wisedu has been tracking and researching a high number of Chinese colleges and universities to develop Counselor Assistant by leveraging over a decade of experience in business system development. Counselor Assistant is an innovative collaboration service focusing on counselor work and dedicated to solving real-world problems.
Industry: Education

## Project Requirements
Currently, Counselor Assistant serves nearly 1,000 schools in China. To sustain the continuously expanding user base, the business database was migrated from the local data center to the cloud. However, as more schools were connected, MySQL instances with up to 6 TB storage capacity could no longer sustain the growing business data, and Ops personnel had to expand the capacity once a week during peak periods. In addition, more students tend to sign in on weekends, generating much more daily written data. However, if MySQL instances with the highest specification were used, the cost would be too high, and the source-replica delay could increase to 30 minutes in worst cases, making it impossible to meet the requirements of read-only businesses such as statistics collection and reporting.

## Solution
The customer eventually selected TDSQL-C for MySQL for the rapid iteration and upgrade of Counselor Assistant. TDSQL-C for MySQL is fully compatible with MySQL, making it easy and worry-free to migrate the original applications with no transformations required.

TDSQL-C for MySQL builds the open-source MySQL database based on TDSQL, Tencent Cloud's distributed cloud storage solution. A single cluster can have up to 128 TB storage capacity, eliminating DBAs' concerns over data volume increase. Read-only nodes can be created within seconds. From Monday to Friday, a cluster with three read-only nodes can meet the business needs. On weekends, the cluster can be quickly scaled out to five read-only nodes, while the source-replica delay is still within milliseconds and the read business is not affected by writes to the source database. Students can now sign in within 1–2 seconds, as compared to 3–5 seconds previously.
![](https://qcloudimg.tencent-cloud.cn/raw/e1094c0bcec17e2e7a9cf5e384305227.png)

## Benefits to Customer
TDSQL-C for MySQL helps Counselor Assistant significantly reduce the user Ops costs and pressure and guarantee a smooth user experience during traffic fluctuations between peak and off-peak hours. Its massive storage capacity and high elasticity solve the pain points of poor scalability of traditional databases, making it much easier for DBAs to run Ops tasks. Moreover, its high performance and concurrency not only double the speed of student sign-in, but also ensure smooth business operations during periodic hours of high numbers of concurrent requests.
