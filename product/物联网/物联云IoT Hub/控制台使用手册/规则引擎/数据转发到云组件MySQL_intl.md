[//]: # (chinagitpath:XXXXX)

### Overview
The rule engine allows you to configure forwarding rules to forward the eligible device-reported data to TencentDB for MySQL. After you create a MySQL instance and table in the [MySQL Console](https://console.cloud.tencent.com/cdb) or through the cloud API, specified fields in device messages can be written to the corresponding MySQL table. The fields specified for writing to the table are highly configurable, and more information about how to configure the written fields is available later in this document (in the Configuring MySQL Instance section). 
The figure below shows the entire process of forwarding data to MySQL by the rule engine:
![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_forward_mysql.png)

### Configuration
1. Log in to the [Rule Engine](https://console.cloud.tencent.com/iotcloud/rules/rule) console page and click the rule you want to configure.
![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_forward_mysql_list_rules.png)

2. Click the **Add Action** button, select the "Data forwarding to TencentDB for MySQL" option and click **Create**.
![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_forward_mysql_select_action.png)
**Note:** You will be prompted to authorize access to the MySQL upon the first use. You need to click **Authorize Now** before you can create.
![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_forwad_mysql_need_auth.png)
![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_forward_mysq_auth_now.png)

3. After the authorization succeeds, you need to configure the MySQL instance information and written field information. As shown in the figure below, the configuration is divided into the following steps:
3.1. Select a region and a MySQL instance. If there is no instance under the account, click "Create instance" to jump to the MySQL Console and create one.
3.2 Enter the username of the MySQL instance just created.     
3.3 Enter the login password of the instance.
3.4. Select the name of the database to write to. If no database has been created under the created MySQL instance, click the "Create database/table" button to jump to the MySQL Console and create a database. For details, see the "Related Documents" section at the end of this document.
3.5 Select the table to write to. If no table has been created under the created database, click the "Create database/table" button to jump to the MySQL Console and create a table.
3.6 Configure the fields to be written. There are two columns here: "field name" and "value". The "field name" corresponds to the field in the database table, indicating the field to be written. The "value" indicates the value of the field to be written. The source of the value can be a message body (which must be in JSON format to support extraction of values) or a constant entered here.
>Note:
>If the source is a message body, use "${}" to reference the fields in the message body. If you want to specify a constant, just enter the corresponding value, such as 5 (number) or hello (string).

![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_forward_mysql_config_instance.png)

### Related Documents
[Create a MySQL database and table](https://cloud.tencent.com/document/product/236/8465)
