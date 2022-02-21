## Overview
After EventBridge is enabled, it will automatically create a **default Tencent Cloud service event bus** in the **Guangzhou** region, and all services connected to it will automatically deliver events. You can also set event rules and delivery targets to configure an alarm link.

## Alarm Configuration Steps
### 1. View the event list
Log in to the [EventBridge console](https://console.cloud.tencent.com/eb), enter the **default Tencent Cloud service event bus**, and view the events of all connected Tencent Cloud services.
![](https://qcloudimg.tencent-cloud.cn/raw/e7e0b0318ff797fc341564324619beb7.png)
![](https://qcloudimg.tencent-cloud.cn/raw/598e6f2078aca989531ceeaa6f71debf.png)

The standard event format is as shown below:
```json
{
    "specversion":"1.0",
    "id":"13a3f42d-7258-4ada-da6d-023a333b4662",
    "source":"${ProductName}.cloud.tencent",
    "type":"cvm:ErrorEvent:ping_unreachable",
    "subject":"${resource ID}",
    "time": 1615430559146,
    "region":"ap-guangzhou",
    "resource":[
        "qcs::eb:ap-guangzhou:uid1250000000:eventbusid/eventruleid"
    ],
    "datacontenttype":"application/json;charset=utf-8",
    "tags":{
        "key1":"value1",
        "key2":"value2"
     },
    "status":"1",
    "data":{
        "appId":"1250000011",
        "instanceId":"ins-sjdksjk",
        "projectId":"11",
        "dimensions":{
            "ip":"127.0.0.1"
            },
        "additionalMsg":{
            "IP":"something unnormal"
            }
    }
}
```

The preceding fields are described as follows:

| Field | Description | Data Type |
| --------------- | ------------------------------------------------------------ | ---------- |
| specversion     | Event structure version (CloudEvents version, which is 1.0.2 currently).        | String     |
| id              | ID returned by `PUT Event`.                                   | String     |
| type            | Type of the event input through `PUT Event`. The standard format of a Tencent Cloud service alarm event is `${ProductName}:ErrorEvent:${EventType}`, where colons are used to separate type fields. | String     |
| source          | Event source (which is required for a Tencent Cloud service event). The value is `xxx.cloud.tencent` by default for a Tencent Cloud service. | String     |
| subject        | Event source details, which can be customized. QCS description such as `qcs::dts:ap-guangzhou:appid/uin:xxx` is used for a Tencent Cloud service by default. | String     |
| timer           | Event time, which is a GMT+0 timestamp in milliseconds such as `1615430559146`.         | Timestamp  |
| datacontenttype | Data structure declaration.                                               | String     |
| region          | Region information.                                                   | String     |
|tags| Resource tag. |JSON|
| data            | Details of the event input through `PUT Event`, which are customizable by the specific business.                                  | JSON    |



### 2. Configure an alarm event rule

Go to the **Event Rule** page, select the target event bus, and create an event rule under it to filter the events for which to configure alarm push.
![](https://qcloudimg.tencent-cloud.cn/raw/58a467fe00eee70c0712b07087ea9f93.png)
Taking CVM alarm configuration as an example, you can select a specified event alarm type as needed or all events.
![](https://qcloudimg.tencent-cloud.cn/raw/709f9b8771ac45a71a82a0b5301f7750.png)

#### Sample alarm rules 
- Receiving all events <br>Set "source" to "cvm.cloud.tencent", which indicates to receive and deliver all alarm events from CVM
   ```json
   {
     "source":"cvm.cloud.tencent"
   }
   ```

- Receiving specified events <br>Only unreachable ping events from CVM are delivered. All other events will be discarded.

   ```json
   {
  "source":"cvm.cloud.tencent",
  "type":"cvm:ErrorEvent:PingUnreachable"
   }
  ```

- Receiving events from the specified instance <br>Receive and deliver events of the CVM resource "ins-XXX". Other events are discarded. The format of "subject" varies for different event source. You can check the formats in the complete event delivered to CLS.
   ```json
   {
  "source":"cvm.cloud.tencent",
  "subject":"ins-xxxxxx"
   }
  ```
   Specifying multiple resources
    ```json
   {
  "source":"cvm.cloud.tencent",
  "subject":["ins-xxxxxx","ins-xxxxxx"]
   }
    ```

For more matching methods, see [Event Pattern](https://intl.cloud.tencent.com/document/product/1108/42288).


### 3. Configure delivery targets

In event alarm scenarios, we recommend you configure two delivery targets: **CLS** and **Notification message**.
<dx-tabs>
::: CLS
EventBridge provides a dedicated CLS log set for the default Tencent Cloud service event bus to deliver your alarm events, which helps you trace back delivered alarm events at any time.
![](https://qcloudimg.tencent-cloud.cn/raw/2c81b965a28d8e14ce725e7f3f510bdf.png)

>? EventBridge offers a free tier of 1 GB per 30 days for storage in the dedicated log set to ensure that you can view and manage basic alarm events free of charge. Excessive storage will be billed according to the CLS billing rules. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/614/37509).

:::
::: Notification message
You can configure a notification message to push your alarm events in the specified delivery method to promptly reach users.
![](https://qcloudimg.tencent-cloud.cn/raw/fd02099eca15edf5accfcc06796a8c33.png)
:::
</dx-tabs>

### 4. Test the configuration result
After completing the configuration, return to the EventBridge console, select the bound event bus, and click **Deliver Event**. You can select a bound event rule template and click **Deliver Event** for test.
>! The test template displays only the `data` field, while other fields are fixed and cannot be customized.

![](https://qcloudimg.tencent-cloud.cn/raw/82adfd70864804faef8ec0f8b23c2156.png)
![](https://qcloudimg.tencent-cloud.cn/raw/2a8eb2b81181a46e9c7de49ebbc49f9f.png)

After completing the configuration, you can view and configure the push of alarm events in the EventBridge console.

#### Sample push content text 

Email content:
```
${ProductName} Alarm Notification
Dear user,

An alarm event occurred for ${ProductName} under your account (ID: ${1}, nickname: ${2}). Please check and resolve the issue in time.

Alarm event: ${EventType}
Alarmed service: ${ProductName}
Alarmed resource: ${Subject}
Alarm region: ${Region}
Event occurrence time: ${Time}
Event status: ${} ("error", "recovered", or "stateless")

For more details, please log in to the EventBridge console.
```

Sample HTTP callback content:
```json
{
"sessionId": "xxxxxxxxxxxxxxxx",  // Event ID
"alarmStatus": "1",//Event.Status
"alarmType": "event",// The value is fixed, indicating an event alarm
"alarmObjInfo": {
   "region": "sh",        // Event region
   "dimensions": {     // Additional description of the resource, which is not fixed and is determined by the respective service (CVM here)
      "unInstanceId": "ins-xxxxx",
      "objDetail": {
                  "deviceLanIp": "xxxx",
                  "deviceWanIp": ""
                  "uniqVpcId": "vpc-xxx"
       },

       "deviceName": "xxx" 
   }
},
"alarmPolicyInfo": { // Alarm policy information, which is compatible with existing CM callbacks
      "policyName": "xxxx",  // EventBridge event rule name
        "conditions": {
            "productName": "cvm",                 // Alarmed service acronym
             "eventName": "guest_reboot",    // Alarm event type
             "alarmNotifyType": "", // It is left empty and is compatible with existing CM callbacks
             "alarmNotifyPeriod": ""  // It is left empty and is compatible with existing CM callbacks
     }
},
"additionalMsg": [{ // Additional information of the alarm event, which is determined by the alarm reporter (CVM here)
"key": "alias",
"value": "xxxx"
}, {
"key": "deviceLanIp",
"value": "xxxx"
}, {
"key": "deviceWanIp",
"value": ""
}, {
"key": "uniqVpcId",
"value": ""
}],
"firstOccurTime": "2021-10-19 11:15:47", // Alarm time
"durationTime": 0,  // Duration
"recoverTime": "0"  // Recovery time

}
```
