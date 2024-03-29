## 操作场景 
对于云服务默认事件集收集到的云服务事件，事件总线支持用户通过配置消息推送，从而实现监控告警事件到用户端的实时推送。
>! 目前消息推送**只支持绑定云服务默认事件集**。

![](https://qcloudimg.tencent-cloud.cn/raw/2a3cd10daa2d3976fbf55a0654e0e442.png)

## 操作步骤 
1. 登录 [事件总线控制台](https://console.cloud.tencent.com/eb)，选择**事件规则** > **云服务默认事件集**，单击**新建事件规则**进行配置。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/113a311524e5a04de86c12cda823d64e.png)
2. 触发方式选择**消息推送**，根据指引配置消息推送的接收用户、接收方式等信息。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/0307108f029b759b73feac750d4c74f3.png)


>! 
>- 使用限制：短信消息限制 500 字，电话限制 350 字。如果您的实例名等字段过长，可能导致消息因长度超限而发送失败，建议您同时配置多个渠道。
>- 跨境进行接口回调可能存在因网络不稳定导致回调失败的情况，请您谨慎选择。

## 消息推送模板

```
云服务产品${产品名称缩写}告警通知
尊敬的腾讯云用户，您好！

您的腾讯云账号（账号 ID：${账号ID}，昵称：${账号名}）云服务服务产品 ${4} 事件告警已触发，请您及时关注并处理。



告警事件：${事件详情}
告警产品：${产品缩写}
告警资源：${资源具体 ID}
告警地域：${资源地域}
事件产生时间：${告警时间}
事件状态：${恢复/未恢复/无状态}

查看更多详情，请登录腾讯云「事件总线」产品控制台查看与管理。
```



## 接口回调示例

>! `DDOS 高防`事件与其他云产品回调的事件结构不同，详情见下。

#### 默认 HTTP 回调内容示例
```json
{
"sessionId": "xxxxxxxxxxxxxxxx",  //事件 ID
"alarmStatus": "1",//Event.Status
"alarmType": "event",//固定，事件告警
"alarmObjInfo": {
   "region": "sh",        //事件地域
   "dimensions": {     //资源补充描述信息，非固定，由每个产品本身决定，此处以 cvm 为例
      "unInstanceId": "ins-xxxxx",
      "objDetail": {
                  "deviceLanIp": "xxxx",
                  "deviceWanIp": ""
                  "uniqVpcId": "vpc-xxx"
       },
       "deviceName": "xxx" 
   }
},
"alarmPolicyInfo": { //告警策略相关，兼容云监控现有回调内容
      "policyName": "xxxx",  //EB事件规则名称
        "conditions": {
            "productName": "cvm",                 //告警产品缩写
             "eventName": "guest_reboot",    //告警事件类型
             "alarmNotifyType": "", //置空，兼容云监控现有回调
             "alarmNotifyPeriod": ""  //置空，兼容云监控现有回调
     }
},
"additionalMsg": [{ //告警事件补充内容，由告警上报方决定，此处以 cvm 为例
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
"firstOccurTime": "2021-10-19 11:15:47", //告警时间
"durationTime": 0,  //持续时间
"recoverTime": "0"  // 恢复时间
}
```

#### DDOS 高防回调内容示例 
```json
{
"id":"xxxxxxxxxxxxxxxx",
"type":"antiddos:ErrorEvent:DDoSAlaram",
"specversion":"1.0",
"source":"antiddos.cloud.tencent",
"subject":"xx.xx.xx.xx",
"time":1662538320000,
"region":"ap-beijing",
"datacontenttype":"application/json;charset=utf-8",
"status":"0",
"tags":null,
"data":{
     "Appid":xxxxxxxxx,
     "InstanceId":"ins-xxx",
     "Ip":"xx.xx.xx.xx",
     "NickName":" xxxxx",
     "Region":"ap-beijing",
     "Uin":"xxxxxxxxxxx"
    }
}
```
