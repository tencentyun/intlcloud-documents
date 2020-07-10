As the restrictions of vendor channels on the push quota and frequency are gradually tightened, the arrival rate and delivery speed of pushes are also limited to a certain degree. For specific restrictions, please see:
- [Vendor Channel Limit Description](https://intl.cloud.tencent.com/document/product/1024/35829)
- [Vendor Channel QPS Limit Description](https://intl.cloud.tencent.com/document/product/1024/35247)

TPNS provides two channel assignment policies: "smart assignment" and "custom", which can improve the comprehensive arrival rate and push speed against the restrictions of the vendor channels.
## Channel Policy Overview
<span id="zhineng"></span>
### Smart assignment
TPNS will take into account the device status, group active status, and push channel status to intelligently assign the optimal delivery channel for each device to achieve the following effects:
1. Improve the comprehensive arrival rate of pushes
2. Improve the comprehensive arrival speed of pushes
3. Save available quotas for certain vendor channels

### Custom policy
Currently, Mi, OPPO, and Vivo channels limit the daily number of pushes. You can choose which channel a certain push task can be delivered through according to your business needs and adjust the push channel delivery policy in a personalized manner to save vendor channel resources and maximize the value of pushes.
The delivery rules of the custom policy are as detailed below:

| Channel | Online | Offline |
|---------|---------|---------|
| Huawei | The vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push | The vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push |
| Meizu | The vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push | The vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push |
| Mi | The TPNS channel is used for push preferably | The vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push |
| OPPO | The TPNS channel is used for push preferably | The vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push |
| Vivo | The TPNS channel is used for push preferably | The vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push |
| Other | TPNS channel | TPNS channel's offline queue |

<span id="zidingyi"></span>

## Getting Started
### Console
You can select a channel policy for a push when creating it in the console. The specific operation path is as follows:
Console > Message Push > Create Push > Advanced Settings > Channel Policy
#### Smart assignment
Select **Smart Assignment** and the system will intelligently assign the delivery channel for each device. For more information, please see the rules of [smart assignment](#zhineng).
![](https://main.qcloudimg.com/raw/b53a8b8e21b37aefea81fe7c8c7553c4.png)

#### Custom policy
Select **Custom** and click **View Details** to view detailed vendor quota information.
![](https://main.qcloudimg.com/raw/a28f612612f856e05bd8e0758805500b.png)
You can choose the channel used for push according to the remaining quota of the current vendor channel and the priority of the push task. For more information, please see the rules of the [custom](#zidingyi) policy.
![](https://main.qcloudimg.com/raw/7b314d96f64fe63dd36b5a1e512389a8.png)

>Note: the TPNS channel cannot be disabled

### REST API
Set the optional `channel_rules` parameter for the REST API. For more information, please see [channel_rules Parameter Description](https://intl.cloud.tencent.com/document/product/1024/33764) in the Push API documentation.
Below is a sample push:
```json
{
    "audience_type": "token",
    "token_list": [
        "05da87c0ae5973bd2dfa9e08d884aada5bb2"
    ],
    "message_type": "notify",
    "channel_rules": [
        {
            "channel": "mz",
            "disable": true
        },
        {
            "channel": "xm",
            "disable": false
        }
    ],
    "message": {
        "title": "Push title",
        "content": "Push content",
        "android": {
             "custom_content":"{\"key\":\"value\"}"
        }
    }
}
```
