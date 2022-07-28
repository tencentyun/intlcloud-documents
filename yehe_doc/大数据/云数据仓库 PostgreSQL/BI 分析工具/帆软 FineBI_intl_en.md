This document describes how to use FineBI with CDWPG to perform visual data analysis on Windows.

## Prerequisites
1. You have created a CDWPG cluster and applied for a public IP as instructed in [Applying for Public IP](https://intl.cloud.tencent.com/document/product/1138/45132).
2. Add your server IP to the CDWPG allowlist as instructed in [Managing IP Allowlist and Blocklist](https://intl.cloud.tencent.com/document/product/1138/45133).
3. Download and install FineBI [here](https://www.finebi.com/product/download).

## Directions
1. Connect to CDWPG and download the JDBC driver as instructed in [Pivotal Greenplum Database Data Connection](https://help.finebi.com/doc-view-289.html).
Download `org.postgresql.Driver` from the page and place the driver package under `%FineBI%\webapps\webroot\WEB-INF\lib` (installation directory on Windows) and restart FineBI.
2. Open the client, set the admin account, select the database, and select **Built-in Database** > **Direct Login**.
3. Select **Management System > Data Connection > Data Connection Management**, click **Create Data Connection**, and select **Pivotal Greenplum Database** under the **All** option.
4. Enter the database connection information:
 - Driver: Select `org.postgresql.Driver`.
 - Database Name: If no database is created in CDWPG, `postgres` will be used by default.
 - Server: You need to add your server IP to the CDWPG allowlist in advance; otherwise, the error message "no pg_hba.conf entry" will be returned.
5. Click **Click to Connect to Database**. After successful connection, you will see the  prompt.
6. Save the data source. You need to select the correct schema. The first schema is pulled by default, which is usually the system schema.
