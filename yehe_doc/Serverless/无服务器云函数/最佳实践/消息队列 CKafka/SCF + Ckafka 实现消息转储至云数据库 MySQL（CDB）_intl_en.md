## Overview

CKafka allows you to dump messages to TencentDB for MySQL to persistently store filtered data.

## Prerequisites

Currently, this feature relies on the SCF and TencentDB for MySQL services, which should be activated first before you can use this feature.

## Directions

Message dump to TencentDB for MySQL will be performed with the CKafka trigger in SCF.

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the instance details page.
3. On the instance details page, select the **Topic Management** tab and click **Message Dump** in the **Operation** column.
4. Click **Add Message Dump** and select **General template** as the dump type.
   - Dump Type: select **General template**.
   - Starting Position: the topic offset of historical messages when dumping.
   - SCF Authorization: indicate your consent to activating SCF and create a function. Then, you need to go to the function settings to set more advanced configuration items and view monitoring information.
5. After the creation is completed, click the **Function Management** link to enter the SCF console for the next step.
6. Upload the code of the CKafkaToMysql template (available on [GitHub](https://github.com/tencentyun/scf-demo-repo/tree/master/Python2.7-CkafkaToMysql)) to the SCF console.
   ![](https://qcloudimg.tencent-cloud.cn/raw/6f2bf000c6ee0c369526fef4f502bbb7.png)
7. Add the following environment variables in **Function Configuration** of the function.
   ![](https://qcloudimg.tencent-cloud.cn/raw/bef67f76d2e2877bb32937cf51f27d70.png)
   
   ```
   dbhost=172.16.0.59 // Databases VPC host address
   dbuser=tabor // Database username
   dbpwd=1237018 // Database password
   dbdatabase=canmengtest // Database name
   dbtable=123321 // Table name
   ```
8. Modify the VPC in **Function Configuration** to make the VPC of the function the same as that of TencentDB.
   ![](https://qcloudimg.tencent-cloud.cn/raw/b8d7e97e7d4a61c2b81ce772d5b183c4.png)
9. In the TencentDB for MySQL DMC console, add the relevant databases, tables, and table structures.
   - Create a database with the same name as in the environment variables:
   - Create a table with the same name as in the environment variables:
   - Create a table structure with the same insertion structure as in the function code. `offset` and `Megs` will be inserted to by default. You can modify the insertion structure on line 33 in the `index.py` file.
     You can also run a TencentDB for MySQL command to directly create tables and data structures:
     
     ```
     CREATE TABLE `test_table` ( `offset` VARCHAR(255) NOT NULL , `Megs` LONGTEXT NOT NULL ) ENGINE = InnoDB;
     ```
10. Enable the CKafka trigger on the trigger management page in the SCF console.


## Restrictions and Billing

- The dump speed is subject to the limit of the peak bandwidth of the CKafka instance. If the consumption is too slow, check the peak bandwidth settings.
- The `CKafkaToMySQL` scheme uses the CKafka trigger. For more information on related settings such as retry policy and maximum number of messages, see [CKafka Trigger](https://intl.cloud.tencent.com/document/product/583/17530).
- When the dump to MySQL feature is used, the dumped messages are the `offset` and `msgBody` data of the CKafka trigger by default. If you want to process the logic by yourself, see [Event Message Structure for CKafka Trigger](https://intl.cloud.tencent.com/document/product/583/17530#ckafka-.E8.A7.A6.E5.8F.91.E5.99.A8.E7.9A.84.E4.BA.8B.E4.BB.B6.E6.B6.88.E6.81.AF.E7.BB.93.E6.9E.84). 
- This feature is provided based on the SCF service that provides a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). For more information on the fees for excessive usage, see the [billing rules](https://intl.cloud.tencent.com/document/product/583/17299) of SCF.
