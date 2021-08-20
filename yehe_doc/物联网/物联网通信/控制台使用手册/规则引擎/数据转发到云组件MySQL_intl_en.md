
## Overview
The rule engine allows you to configure forwarding rules to forward eligible data reported by devices to TencentDB for MySQL. After you create an instance and table in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) or through TencentCloud API, specified fields in device messages can be written to the corresponding TencentDB for MySQL table.

The figure below shows the entire process of forwarding data to TencentDB for MySQL by the rule engine:
![](https://main.qcloudimg.com/raw/9012b5275680b170ec6cc8b69358664f.png)

## Configuration
1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud) and click **Rule Engine** on the left sidebar.
2. Go to the rule engine page and click the rule to be configured.
3. On the rule details page, click **Add Action**.
>?You will be prompted to authorize access to TencentDB for MySQL upon the first use. You need to click **Authorize Now** before you can proceed.
![](https://main.qcloudimg.com/raw/801f85ef547eb49e222c69c9be971a5c.png)
4. In the **Add Action** pop-up window, select **Forward data to TencentDB for MySQL**. After successful authorization, you need to configure the information of the TencentDB for MySQL instance and written fields as shown below. The configuration is divided into the following steps:
![](https://main.qcloudimg.com/raw/4cc5fa04e89821138a0e6362280bb6cb.png)
After successful forwarding, the information displayed in TencentDB for MySQL is as shown below:
![](https://main.qcloudimg.com/raw/d2de60c73ee63f5c3d21080e9fce535b.png)

## Configuration Description
The configuration is divided into the following steps:
 1. Select the region and TencentDB for MySQL instance.
 2. Enter the username of the TencentDB for MySQL instance you just created.     
 3. Enter the login password of the instance.
 4. Select the name of the database to be written to. If no database has been created under the created TencentDB for MySQL instance, go to the TencentDB for MySQL console to create one. For detailed directions, please see [DMC Overview](https://intl.cloud.tencent.com/document/product/236/39221).
 5. Select the table to be written to. If no table has been created under the created database, go to the TencentDB for MySQL console to create one.
 6. Configure the fields to be written. There are two columns here: "field name" and "value". "Field name" corresponds to the field in the database table, indicating the field to be written. "Value" indicates the value of the field to be written. The value source can be a message body (which must be in JSON format to support value extraction) or a constant entered here.
    >!
     >- If the source is a message body, use "${}" to import the fields in the message body. If you want to specify a constant, just enter the corresponding value, such as 5 (number) or hello (string).
     >- You must create the database, table, and fields in TencentDB for MySQL first before you can write data to the database.


For more information, please see [DMC Overview](https://intl.cloud.tencent.com/document/product/236/39221).

## Resending Mechanism

The resending mechanism is used to send the message again in case of a failure in the message forwarding process, which makes sure that the message is received. The details are as follows:
- If message forwarding fails, the system will retry forwarding at intervals of 1s, 3s, and 10s in sequence. If all three retries fail, the message will be discarded.
- If you have configured the "action for forwarding failure", then after three unsuccessful retries, the message will be forwarded again according to the configured action. If forwarding still fails, the message will be discarded.
