This document describes how to initialize a TencentDB for MySQL instance for convenient use.

## Prerequisites
1. You have registered a Tencent Cloud account and verified your identity.
To register a Tencent Cloud account:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Click here to register a Tencent Cloud account</a></div>
To verify your identity:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Click here to verify your identity</a></div>
2. You have purchased a TencentDB for MySQL instance.
To purchase a TencentDB for MySQL instance:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://buy.cloud.tencent.com/cdb" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn3">Click here to enter the purchase page</a></div>

## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) and select **Instance List** on the left sidebar.
3. Select a TencentDB for MySQL instance in **Uninitialized** status and click **Initialize** in the "Operation" column.
![](https://main.qcloudimg.com/raw/945a4e69bef68eb706a520d4cbac13cf.png)
4. In the initialization dialog box that pops up, configure the parameters related to initialization, and click **OK** to start initialization.
 - **Supported character set**: LATIN1, GBK, UTF8, and UTF8MB4 character sets are supported. The default value is LATIN1, i.e., ISO-8859-1 encoding format. After initializing the instance, you can also change the character set on the instance details page in the console.
 - **Table name case sensitivity**: set whether the table name is case-sensitive, which is yes by default.
 - **Custom port**: the database access port, which is 3306 by default.
 - **Set password for root account**: the username of the newly created TencentDB for MySQL instance is `root` by default. Set a password for this `root` account.
 - **Confirm password**: enter the password again.
5. Return to the instance list. The status of the target TencentDB for MySQL instance has changed to **Running**, indicating that the initialization was successful.
