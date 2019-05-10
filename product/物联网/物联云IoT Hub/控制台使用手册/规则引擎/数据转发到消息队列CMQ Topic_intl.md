[//]: # (chinagitpath:XXXXX)

### Overview
The rule engine allows you to configure rules to forward eligible device-reported data to the CMQ topic queue. After subscribing to a topic in the [CMQ Console](https://console.cloud.tencent.com/mq/topic?rid=1) or via the cloud API, you will receive message notifications from the CMQ topic. The CMQ topic message notification feature enables asynchronous message reception.
The figure below shows the entire process of forwarding data to a CMQ topic by the rule engine:
![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_cmq_topic.png)


### Configuration
1. Log in to the [Rule Engine](https://console.cloud.tencent.com/iotcloud/rules/rule) console page and click the rule you want to configure.
![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_cmqtopic01.png)

2. Click the **Add Action** button, select the "Data forwarding to CMQ topic" option, select the region and topic and click **Create**.
![image](https://main.qcloudimg.com/raw/b44562eacac2546ce6cc6b63f159110e.png)


**Note:** You need to authorize CMQ topic access if you are using it for the first time. You need to click **Authorize now** to be able to create.
![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_cmqtopic03.png)

![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_cmqtopic04.png)



### Related Documents
 [Create CMQ topic subscription using the cloud API](https://cloud.tencent.com/document/api/406/5853)

