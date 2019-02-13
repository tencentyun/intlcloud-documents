[//]: # (chinagitpath:XXXXX)

### Overview
The rule engine allows you to configure rules to forward the eligible device-reported data to a CMQ topic. After you subscribe to the topic in the [CMQ Console](https://console.cloud.tencent.com/mq/topic?rid=1) or through the cloud API, you can receive the messages pushed from the topic. The message push mechanism of the CMQ topic provides a highly reliable ability to receive messages asynchronously.
The figure below shows the entire process of forwarding data to a CMQ topic by the rule engine:
![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_cmq_topic.png)


### Configuration
1. Log in to the [Rule Engine](https://console.cloud.tencent.com/iotcloud/rules/rule) console page and click the rule you want to configure.
![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_cmqtopic01.png)

2. Click the **Add Action** button, select the "Data forwarding to CMQ topic" option, select the region and topic and click **Create**.
![image](https://main.qcloudimg.com/raw/b44562eacac2546ce6cc6b63f159110e.png)


**Note:** You will be prompted to authorize access to the CMQ topic upon the first use. You need to click **Authorize Now** before you can create.
![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_cmqtopic03.png)

![image](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/iot_cmqtopic04.png)



### Related Documents
 [Create a CMQ topic subscription using the cloud API](https://cloud.tencent.com/document/api/406/5853)

