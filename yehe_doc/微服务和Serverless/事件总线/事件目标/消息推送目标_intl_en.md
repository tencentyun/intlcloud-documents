## Overview 
For Tencent Cloud service events collected by the default Tencent Cloud service event bus, EventBridge allows you to configure message push to push Cloud Monitor events to user terminals in real time.
>! Currently, message push **can only be bound to the default Tencent Cloud service event bus**.

![](https://qcloudimg.tencent-cloud.cn/raw/2a3cd10daa2d3976fbf55a0654e0e442.png)

## Directions 
1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb), choose **Event Rule**, select **Default Tencent Cloud service event bus**, and click **Create Event Rule**.
![](https://qcloudimg.tencent-cloud.cn/raw/113a311524e5a04de86c12cda823d64e.png)
2. Set **Trigger** to **Notification message**, and set **Recipients**, **Delivery Method**, and other information as prompted.
![](https://qcloudimg.tencent-cloud.cn/raw/0307108f029b759b73feac750d4c74f3.png)


>! 
>- Use limits: For SMS message delivery, a notification message can contain up to 500 characters. For phone delivery, a notification message can contain up to 350 characters. If fields such as the instance name are too long, notification messages may fail to be sent due to excessive length. You are advised to configure multiple delivery channels at the same time.
>- Cross-MLC-border API callback may fail due to network instability. 

## Message Push Template

```
Tencent Cloud ${Service name abbreviation} Alert
Dear Tencent Cloud user,

An alert is triggered for Tencent Cloud ${4} under your account (Account ID: ${Account ID}; Name: ${Account name}). Check and resolve the issue in time.



Alerted event: ${Event details}
Alerted service: ${Service name abbreviation}
Alerted resource: ${Resource ID}
Alarm region: ${Resource region}
Event generation time: ${Alarm time}
Event status: ${Recovered/Not recovered/Stateless}

For more details, log in to the EventBridge console.
```



## Callback Samples

>! DDoS event callbacks are different from others. 

#### Default HTTP callback
```json
{
"sessionId": "xxxxxxxxxxxxxxxx",  // Event ID
"alarmStatus": "1",//Event.Status
"alarmType": "event",// The value is fixed, indicating an event alarm
"alarmObjInfo": {
   "region": "sh",        // Event region
   "dimensions": {     // Additional description of the resource, which is subjected to the related Tencent Cloud service (CVM here)
      "unInstanceId": "ins-xxxxxxxx",
      "objDetail": {
                  "deviceLanIp": "xxxx",
                  "deviceWanIp": ""
                  "UniqVpcId": "vpc-xxxxxx"
       },
       "DeviceName": "xx", 
   }
},
"alarmPolicyInfo": { // Alarm policy information, which is compatible with existing CM callbacks
      "policyName": "xxxx",  // EventBridge event rule name
        "conditions": {
            "productName": "cvm",                 // Abbreviation of the related Tencent Cloud service
             "eventName": "guest_reboot",    // Event type
             "alarmNotifyType": "", // It is left empty and is compatible with existing CM callbacks
             "alarmNotifyPeriod": ""  // It is left empty and is compatible with existing CM callbacks
     }
},
"additionalMsg": [{ // Additional information of the event, which is determined by the event reporter (CVM here)
"key": "alias",
"value": "xxxx"
}, {
"Key": "deviceLanIp",
"value": "xxxx"
}, {
"Key": "deviceWanIp",
"Value":
}, {
"Key": "uniqVpcId",
"Value":
}],
"firstOccurTime": "2021-10-19 11:15:47", // Alerted time
"durationTime": 0,  // Duration
"recoverTime": "0"  // Recovery time
}
```

#### DDoS Callback Sample 
```json
{
"id":"xxxxxxxxxxxxxxxx",
"type":"antiddos:ErrorEvent:DDoSAlaram",
"specversion":"1.0",
"source":"antiddos.cloud.tencent",
"subject":"xx.xx.xx.xx",
"time": 1615430559146,
"Region":"ap-beijing",
"datacontenttype":"application/json;charset=utf-8",
"status":"0",
"tags":null,
"data":{
     "Appid":xxxxxxxxx,
     "InstanceId": "ins-xxx",
     "Ip":"xx.xx.xx.xx",
     "NickName":" xxxxx",
     "Region":"ap-beijing",
     "Uin":"xxxxxxxxxxx"
    }
}
```
