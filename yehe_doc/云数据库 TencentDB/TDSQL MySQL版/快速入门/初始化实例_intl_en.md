
After creating a TDSQL for MySQL instance, you need to initialize it before you can use it.

## Directions
1. Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/dcdb), select a region, locate the uninitialized instance in the instance list, and click **More** > **Initialize** in the **Operation** column.
2. In the pop-up dialog box, select the configuration as needed, and click **OK**.
 - Supported character sets: select the character set supported by MySQL.
 - Case-sensitive table name: set whether the table name of database is case-sensitive.
 - Enable strong sync: enable strong sync to ensure data consistency at the secondary node in case the primary node fails. At least 2 nodes are required for this option to work.
![](https://main.qcloudimg.com/raw/2deee0a9b8a0bbc564b3ef1a290f060c.png)
3. Return to the instance list to locate the instance. When the status changes **Running**, the instance can be connected.

## Instance Connection
After initialization, you can access the TDSQL for MySQL instance over both the private and public networks from a Windows or Linux CVM instance. For more information, please see [Connecting to Instances](https://intl.cloud.tencent.com/document/product/1042/33338).
