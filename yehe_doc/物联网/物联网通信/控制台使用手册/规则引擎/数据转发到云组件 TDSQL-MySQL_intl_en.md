## Overview

The rule engine allows you to configure forwarding rules to forward eligible data reported by devices to TDSQL for MySQL. After you create an instance and table in the [TDSQL for MySQL console](https://console.cloud.tencent.com/tdsqld/instance-tdmysql) or through TencentCloud API, specified fields in device messages can be written to the corresponding TDSQL for MySQL table.

The figure shows the entire process of forwarding data to TDSQL for MySQL by the rule engine:
![](https://qcloudimg.tencent-cloud.cn/raw/93912c72f36af6c46d8fa6d75b5b5858.jpg)

## Configuration[](id:test)

1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud) and click **Rule Engine** on the left sidebar.
2. Click the **Rule Name** of the rule to be configured.
3. Click **Add Action**. You will be prompted to authorize access to the TDSQL instance if this is your first time using the rule engine. Click **Authorize Now** and continue to create.
<img src="" style="width: 75%;">
4. After successful authorization, in the **Add Action** pop-up window, select **Forward data to TDSQL for MySQL**. You need to configure the information of the TDSQL for MySQL instance and written fields as shown below. The configuration is divided into the following steps:
<img src="" style="width: 75%;">
5. After completing the configuration, click **Save**.


## Configuration Description

The [configuration](#test) is divided into the following steps:
1. Select a region and a TDSQL for MySQL instance.
2. Enter the username of the TDSQL for MySQL instance you just created.     
3. Enter the login password of the instance.
4. Select the name of the database to be written to. If no database has been created under the created TDSQL for MySQL instance, go to the TDSQL for MySQL console to create one.
5. Select the table to be written to. If no table has been created under the created database, go to the TDSQL for MySQL console to create one.
6. Configure the fields to be written. There are two columns here: "field name" and "value". "Field name" corresponds to the field in the database table, indicating the field to be written. "Value" indicates the value of the field to be written. The value source can be a message body (which must be in JSON format to support value extraction) or a constant entered here.
<dx-alert infotype="notice" title="">
- If the source is a message body, use `"${}"` to import the fields in the message body. If you want to specify a constant, just enter the corresponding value, such as 5 (number) or hello (string).
- You must create the database, table, and fields in TDSQL for MySQL first before you can write data to the database.
</dx-alert>




## Resending Mechanism

The resending mechanism is used to send the message again in case of a failure in the message forwarding process, which makes sure that the message is received. The details are as follows:
- If message forwarding fails, the system will retry forwarding at intervals of 1s, 3s, and 10s in sequence. If all three retries fail, the message will be discarded.
- If you have configured the **Forward Error Action** item, then after three unsuccessful retries, the message will be forwarded again according to the configured action. If forwarding still fails, the message will be discarded.
