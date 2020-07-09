As OPPO, Vivo, Mi, and other vendors have successively announced quota limits for push messages, in order to more reasonably assign vendor channel resources, TPNS has launched a task-level channel policy feature. You can determine the channel assignment for each push task based on the current remaining quota for the corresponding vendor channel to increase the arrival rate.
## Channel Policy Overview
TPNS currently provides two channel policies, i.e., smart assignment and custom channel. The channel policy rules are as shown below:

<span id="zhineng"></span>
### Smart assignment
The system intelligently assigns the delivery channel for each device on the basis of guaranteeing the push arrival rate in order to save vendor channel resources.

| Channel | Online | Offline |
|---------|---------|---------|
| Huawei | The vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push | The vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push |
| Meizu | The vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push | The vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push |
| Mi | The TPNS channel is used for push preferably | The vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push |
| OPPO | The TPNS channel is used for push preferably | The vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push |
| Vivo | The TPNS channel is used for push preferably | The vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push |
| Other | TPNS channel | TPNS channel's offline queue |

<span id="zidingyi"></span>
### Custom policy
As the resources of certain vendor channels are limited, you can choose the channel through which a push will be delivered according to your business needs. For more information on the vendor channel quotas, please see [Vendor Channel Limit Description](https://intl.cloud.tencent.com/document/product/1024/35829).

| Channel | Enabled | Disabled |
|---------|---------|---------|
| Huawei | <li>Online: the vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push <li>Offline: the vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push | <li>Online: TPNS channel <li>Offline: TPNS channel |
| Meizu | <li>Online: the vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push <li>Offline: the vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push | <li>Online: TPNS channel <li>Offline: TPNS channel |
| Mi | <li>Online: the TPNS channel is used for push preferably <li>Offline: the vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push | <li>Online: TPNS channel <li>Offline: TPNS channel |
| OPPO | <li>Online: the TPNS channel is used for push preferably <li>Offline: the vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push | <li>Online: TPNS channel <li>Offline: TPNS channel |
| Vivo | <li>Online: the TPNS channel is used for push preferably <li>Offline: the vendor channel is used for push preferably, and if it fails, the TPNS channel will be used to retry the push | <li>Online: TPNS channel <li>Offline: TPNS channel |
| Other | <li>Online: TPNS channel <li>Offline: TPNS channel offline queue | <li>Online: TPNS channel <li>Offline: TPNS channel </li> |

## Getting Started
### Console
After entering the push content, you can select a policy in the channel policy section in **Message Push** > **Create Push** > **Advanced Settings** in the console.
#### Smart assignment
Select **Smart Assignment** and the system will intelligently assign the delivery channel for each device. For more information, please see the rules of [smart assignment](#zhineng).
![](https://main.qcloudimg.com/raw/d06fadff60969ef71c87fd20cd6f97d9.png)

#### Custom policy
Select **Custom** and click **View Details** to view detailed vendor quota information.
![](https://main.qcloudimg.com/raw/9cac2ce60ed7718b5c29a48ee35565ac.png)
You can choose the channel used for push according to the remaining quota of the current vendor channel and the priority of the push task. For more information, please see the rules of the [custom](#zidingyi) policy.
![](https://main.qcloudimg.com/raw/9200f87b9d5114bedee4a3f3f83757fc.png)

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
