## Table Group Overview
As a logic isolation method in TcaplusDB, a table group represents a data partition that can separate different tables from each other. A cluster can contain multiple table groups, and a table group can contain multiple tables. Different table groups cannot access data of each other.

From the perspective of gaming business, if a gaming business supports unified servers in all zones and can read/write the same table group in the cluster, then it does not need to be divided into different zones. It can also be server-specific/zone-specific, i.e., the cluster can contain multiple table groups.

## Creating Table Group
For detailed directions, please see [Creating Table Group](https://intl.cloud.tencent.com/document/product/1016/32716).

## Table Group Details
You can view the table group configuration and attributes on the cluster list page to understand the overall cluster usage.
You can log in to the [TcaplusDB Console](https://console.cloud.tencent.com/tcaplusdb/app) and enter the cluster list to view the table group information of the target cluster.

Table group information contains the following four fields:
- ID: it is the ID of the table group in the current cluster, which is required during database connection. Please note that the table group IDs may be repeated in different clusters.
- Table Group Name: you can customize the name of the table group based on its actual purpose.
- Table Count: it indicates the number of tables in the current table group.
- Total Capacity: it indicates the disk capacity used by the tables in the current table group.
