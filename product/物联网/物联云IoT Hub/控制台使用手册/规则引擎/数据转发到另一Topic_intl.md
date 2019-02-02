[//]: # (chinagitpath:XXXXX)

## Overview
Machine-to-machine (M2M) communication among different devices can be achieved by forwarding the desired message fields to another topic. Topic can be entered in three ways:
- **Enter a topic name**
For example, ```${productId}/house_monitor/thermometer```, indicating that the messages that satisfy the rule will be forwarded to this topic.
- **Enter a topic name with variables**
For example, ```${procductId}/${house}/device```, where ```house``` in the ```${}``` represents a variable name, which is the content of the field selected in the SELECT statement.
- **Enter a topic name with functions**
For example, ```${procductId}/${house}/topic(1)```, where ```topic(1)``` is to take out the first level of data in the source topic which is the topic in the FROM statement.

Below is an example of how a forwarding topic with variables works. Assume that the following rule is defined:

```
SELECT temperature as t, house 
FROM house_monitor/thermometer/get 
WHERE house="tencent" AND temperature > 40
```

This rule extracts the values of the two fields ```t``` and ```house``` from the message. Assume that the content of the field ```house``` is ```tencent```. If you define forwarding to the topic ```house_monitor/app/{house}```, the rule engine will replace the "${house}" variable in this topic with "tencent", which will send the values of the fields ```t``` and ```house``` to the topic ```house_monitor/app/tencent```.

The figure below shows the whole process of forwarding:
![image](https://mc.qcloudimg.com/static/img/2fd61f602479ab39f47e7d6eb4f93558/gui3.png)
## Configuration
1. Log in to the [Rule Engine](https://console.cloud.tencent.com/iotcloud/rules/rule) console page and click the rule you want to configure.
![](https://main.qcloudimg.com/raw/0a0a0e5bc48aa0d4492ac0b8d3c7413c.png)
2. On the rule details page, click the **Add Action** button. In the "Add Action" window that pops up, select the action "republish", enter the name of the topic to forward to and click **Create**. The IoT Hub platform will forward the reported data to this topic.
![image](https://main.qcloudimg.com/raw/1b87e2ca055b5d0581c2fe7e6568c8fb.png)

