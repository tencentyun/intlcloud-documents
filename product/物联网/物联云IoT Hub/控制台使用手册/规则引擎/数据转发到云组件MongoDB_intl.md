[//]: # (chinagitpath:XXXXX)

### Overview
The rule engine allows you to configure forwarding rules to forward the eligible device-reported data to TencentDB for MongoDB. After you create a MongoDB instance in the [MongoDB Console](https://console.cloud.tencent.com/mongodb) or through the cloud API, device messages can be written to the corresponding MongoDB collection.
The figure below shows the entire process of forwarding data to MongoDB by the rule engine:
![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_forward_mongodb.png)


### Configuration
1. Log in to the [Rule Engine](https://console.cloud.tencent.com/iotcloud/rules/rule) console page and click the rule you want to configure.
![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_forward_mysql_list_rules.png)

2. Click the **Add Action** button, select the "Data forwarding to TencentDB for MongoDB" option and click **Create**.
![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_forward_mongodb_select_action.png)  
**Note:** You will be prompted to authorize access to the MongoDB upon the first use. You need to click **Authorize Now** before you can create.
![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_forwad_mongodb_need_auth.png)
![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_forwad_mongodb_now_auth.png)

3. Upon authorization, you need to configure the MongoDB instance information. As shown in the figure below, the configuration is divided into the following steps:

    1. Select region and MySQL instance. If there is no instance under the account, click "Create instance" to jump to the MongoDB Console and create one.
    2. Enter the username of the MongoDB instance (mongouser by default at MongoDB's official website).     
    3. Enter the login password of the MongoDB instance.
    4. Enter the name of the database to write to.
    5. Enter the name of the collection to write to.
![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_forward_mongodb_config_instance.png)

