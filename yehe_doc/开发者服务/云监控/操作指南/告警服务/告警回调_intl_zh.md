通过接口回调，您的企业微信群或自建系统可以直接收到云监控的告警通知。接口回调具备将告警信息通过 HTTP 的 POST 请求推送到可访问公网 URL 的功能，您可基于接口回调推送的告警信息做进一步的处理。如需通过企业微信群接收告警通知，请参见 [配置企业微信群接收告警通知](https://intl.cloud.tencent.com/document/product/248/38208)。

> ? 
> - 回调地址保存后自动验证一次您的 URL，验证超时时间为5s；当用户创建的告警策略被触发或被恢复均会通过接口回调推送告警消息，此告警消息最多推送三次， 每次请求的超时时间为5s。
> - 当用户创建的告警策略被触发或恢复时，均会通过接口回调推送告警消息。接口回调也支持重复告警。

## 操作步骤

1. 进入 [云监控控制台—告警策略](https://console.cloud.tencent.com/monitor/policylist/ )。
2. 选择对应的告警策略，进入告警策略管理页。
3. 在接口回调模块中填写公网可访问的告警回调 URL。
   ![](https://main.qcloudimg.com/raw/6c5dcf93ba7498f44faa33dbbcaa82ad.png)
4. HTTP 返回 200为验证成功。当回调 URL 验证成功后，云监控会将告警消息通过 HTTP 的 POST 请求推送您系统的URL地址，您可以参考 [告警回调参数说明](#.E5.91.8A.E8.AD.A6.E5.9B.9E.E8.B0.83.E5.8F.82.E6.95.B0.E8.AF.B4.E6.98.8E)，对推送的告警信息做进一步的处理。


## 告警回调参数说明

当告警规则被触发时，云监控会将告警消息发送到您系统的 URL 地址。接口回调通过 HTTP 的 POST 请求发送 JSON 格式的数据，您可以根据下列参数说明对告警信息做进一步的处理。

#### 指标告警

#### 指标告警参数示例

```
{
       "sessionId": "xxxxxxxx",
       "alarmStatus": 1,    // 1为告警，0为恢复
       "alarmType":"metric",    // 告警类型（"metric": 指标告警，"event": 事件告警）
       "alarmObjInfo": {
            "region": "gz",  // 不分地域的产品不返回该字段
            "namespace": "qce/cvm",      // 产品的名字空间
            "dimensions": {               // dimensions字段里的内容不同产品有差异
                "unInstanceId": "ins-o9p3rg3m",  
                "objId":"xxxxxxxxxxxx"
            }
       },
       "alarmPolicyInfo": {
                "policyId": "policy-n4exeh88",   // 告警策略组ID
                "policyType": "cvm_device",     // 告警策略类型名
                "policyName": "test",      // 告警策略组名称
                "policyTypeCName": "云服务器-基础监控",      // 告警策略类型展示名称
                "conditions": {
                    "metricName": "cpu_usage",         // 指标名称
                    "metricShowName": "CPU 利用率",       // 指标展示名称（中文名）
                    "calcType": ">",              // 比较方式（无阈值的指标不返回该字段）
                    "calcValue": "90",            // 告警阈值（无阈值的指标不返回该字段）
                    "currentValue": "100",       // 当前告警值（无阈值的指标不返回该字段）
                    "unit": "%",                 // 单位（无阈值的指标不返回该字段）
                    "period": "60",              // 统计周期（单位：s；无阈值的指标不返回该字段）
                    "periodNum": "1",            // 持续周期（无阈值的指标不返回该字段）
                    "alarmNotifyType": "continuousAlarm",    // 是否支持重复告警（"singleAlarm": 不重复告警，"exponentialAlarm": 指数周期告警，"continuousAlarm": 持续告警，无阈值的指标不返回该字段）
                    "alarmNotifyPeriod": 300                 // 重复告警的频率（单位: s；无阈值的指标不返回该字段）
                }
        },
        "firstOccurTime": "2017-03-09 07:00:00",     // 第一次触发告警的时间
        "durationTime": 500,       // 告警持续时间（单位：s；未恢复时为第一次触发告警后截止到此次发送告警的时间）
        "recoverTime": "0"     // 告警恢复时间（单位：s；未恢复时为0）
}
```

#### 指标告警 dimensions 示例

**云服务器 CVM**

```
"dimensions": {
    "unInstanceId": "ins-xxxxxxxx",
    "objId": "94f1133c-46cf-4c61-a4c1-d928183aba47",       // 后台绑定的实例维度
    "objName": "172.21.30.15#588789"       // 告警短信内返回的实例相关信息
}
```

**负载均衡 LB-外网监听器**

```
"dimensions": {
    "protocol": "https",
    "vip": "118.25.31.161",
    "vport": 443,
    "objId": "118.25.31.161#443#https",       // 后台绑定的实例维度
    "objName": "CAuthCenteH5 | 基础网络 | 118.25.31.161(https:443)"       // 告警短信内返回的实例相关信息
}
```

**负载均衡 LB-内网监听器**

```
"dimensions": {
    "protocol": "",
    "vip": "",
    "vpcId": 123,
    "vport": "",
    "objId": "xxx",       // 后台绑定的实例维度
    "objName": "xxx"       // 告警短信内返回的实例相关信息
}
```

**负载均衡 LB-外网服务器端口**

```
"dimensions": {
    "domain": "",
    "unLoadBalancerId": "",
    "protocol": "",
    "lanIp": "",
    "port": "",
    "url": "",
    "vip": "",
    "vpcId": 123,
    "loadBalancerPort": "",
    "objId": "xxx",       // 后台绑定的实例维度
    "objName": "xxx"       // 告警短信内返回的实例相关信息
}
```

**负载均衡 LB-内网服务器端口**

```
"dimensions": {
    "protocol": "",
    "lanIp": "",
    "port": "",
    "vip": "",
    "vpcId": 123,
    "loadBalancerPort": "",
    "objId": "xxx",       // 后台绑定的实例维度
    "objName": "xxx"       // 告警短信内返回的实例相关信息
}
```

**云数据库 MySQL-主机监控**

```
"dimensions": {
    "uInstanceId": "xxx",
    "objId": "xxx",       // 后台绑定的实例维度
    "objName": "xxx"       // 告警短信内返回的实例相关信息
}
```

**云数据库 MySQL-备机监控**

```
"dimensions": {
    "uInstanceId": "xxx",
    "objId": "xxx",       // 后台绑定的实例维度
    "objName": "xxx"       // 告警短信内返回的实例相关信息
}
```

**云数据库 Redis**

```
"dimensions": {
    "redis_uuid": "xxx",
    "objId": "xxx",       // 后台绑定的实例维度
    "objName": "xxx"       // 告警短信内返回的实例相关信息
}
```

**专线接入-物理专线**

```
"dimensions": {
     "directconnectid": "xxx",
     "objId": "xxx",       // 后台绑定的实例维度
     "objName": "xxx"       // 告警短信内返回的实例相关信息
}
```

**专线接入-专用通道**

```
"dimensions": {
    "directconnectconnid": "dcx-jizf8heu",
    "objId": "dcx-jizf8heu",       // 后台绑定的实例维度
    "objName": "dcx-jizf8heu"       // 告警短信内返回的实例相关信息
}
```

**私有网络-专线网关**

```
"dimensions": {
    "directconnectgatewayid": "dcg-8wo1p2ve",
    "objId": "dcg-8wo1p2ve",       // 后台绑定的实例维度
    "objName": "dcg-8wo1p2ve"       // 告警短信内返回的实例相关信息
}
```

**专线接入-专用通道**

```
"dimensions": {
    "directconnectconnid": "xxx",
    "objId": "xxx",       // 后台绑定的实例维度
    "objName": "xxx"       // 告警短信内返回的实例相关信息
}
```

**私有网络-NAT 网关**

```
"dimensions": {
    "uniq_nat_id": "xxx",
    "objId": "xxx",       // 后台绑定的实例维度
    "objName": "xxx"       // 告警短信内返回的实例相关信息
}
```

**私有网络-VPN 通道**

```
"dimensions": {
    "vpnconnid": "xxx",
    "objId": "xxx",       // 后台绑定的实例维度
    "objName": "xxx"       // 告警短信内返回的实例相关信息
}
```

**私有网络-对等连接**

```
"dimensions": {
    "peeringconnectionid": "xxx",
    "objId": "xxx",       // 后台绑定的实例维度
    "objName": "xxx"       // 告警短信内返回的实例相关信息
}
```

**私有网络-基础网络跨地域互联**

```
"dimensions": {
    "peeringconnectionid": "xxx",
    "objId": "xxx",       // 后台绑定的实例维度
    "objName": "xxx"       // 告警短信内返回的实例相关信息
}
```

**私有网络-专线网关**

```
"dimensions": {
    "directconnectgatewayid": "xxx",
    "objId": "xxx",       // 后台绑定的实例维度
    "objName": "xxx"       // 告警短信内返回的实例相关信息
}
```

**私有网络-VPN 网关**

```
"dimensions": {
    "appid": 12345,
    "vip": "10.0.0.0",
    "objId": "xxx",       // 后台绑定的实例维度
    "objName": "xxx"       // 告警短信内返回的实例相关信息
}
```

**私有网络-网络探测**

```
"dimensions": {
    "appid": 12345,
    "netdetectid": "xxx",
    "vpcid": "xxx",
    "objId": "xxx",       // 后台绑定的实例维度
    "objName": "xxx"       // 告警短信内返回的实例相关信息
}
```

**私有网络-共享带宽包**

```
"dimensions": {
    "__region__": "xxx",
    "appid": 12345,
    "netgroup": "xxx",
    "objId": "xxx",       // 后台绑定的实例维度
    "objName": "xxx"       // 告警短信内返回的实例相关信息
}
```

#### 事件告警

##### 事件告警参数示例

```
{
    "sessionId":"vuRH4ZlxBJSMNJHvNZhls9HY",
    "alarmStatus":"1",    // 1为告警，0为恢复
    "alarmType":"event",    // 告警类型（"metric": 指标告警，"event": 事件告警）
    "alarmObjInfo":{
        "region":"gz",      // 不分地域的产品不返回该字段
        "dimensions":{               // dimensions字段里的内容不同产品有差异
            "unInstanceId":"ins-pftdvqa2",
            "objDetail":{         // 事件告警对象详情
                "deviceLanIp":"172.21.0.17",
                "deviceWanIp":"118.89.233.99",
                "uniqVpcId":"vpc-ilrwkcbw"
            }
        }
    },
    "alarmPolicyInfo":{
        "policyId":"policy-n4exeh88",   // 告警策略组ID
        "policyType":"cvm_device",     // 告警策略类型名
        "policyName":"teset",      // 告警策略组名称
        "conditions":{
            "productName":"cvm",      // 产品类型名
            "productShowName":"云服务器",      // 产品类型展示名
            "eventName":"ping_unreachable",      // 事件名称
            "eventShowName":"ping不可达",      // 事件名称
            "alarmNotifyType":"singleAlarm",    // 是否支持重复告警（"singleAlarm": 不重复告警，"exponentialAlarm": 指数周期告警，"continuousAlarm": 持续告警，无阈值的指标不返回该字段）
            "alarmNotifyPeriod":"0"                 // 重复告警的频率（单位: s；无阈值的指标不返回该字段）
        },
        "policyTypeCName":"云服务器-基础监控"      // 告警策略类型展示名称
    },
    "firstOccurTime":"2018-06-15 16:32:06",     // 第一次触发告警的时间
    "recoverTime":"0"      // 告警恢复时间（单位：s；未恢复的告警/无恢复状态的告警为0）
}
```

##### 事件告警 dimensions 示例

**云服务器**

```
"dimensions":{
    "unInstanceId":"ins-pftdvqa2",
    "objDetail":{         // 事件告警对象详情
       "deviceLanIp":"172.21.0.17",
       "deviceWanIp":"118.89.233.99",
       "uniqVpcId":"vpc-ilrwkcbw"
            }
        }
```

**云数据库 MySQL**

```
"dimensions": {
      "deviceName": "production-xd_item_center-0-offline-6035",
      "objDetail": {
        "IP": "10.80.17.217"
      },
      "unInstanceId": "cdb-bwieva60"
    }  
```

**私有网络-对等连接**

```
"dimensions":{
    "unInstanceId":"pcx-142mpvfc",
    "objDetail":{         // 事件告警对象详情
        "PeeringConnectionName":"test-VPC1 <--> test-VPC3",
        "QosBandwidth":"100Mps",
        "VpcName":"test-VPC1",
        "VpcId":"vpc-5x1u9jq8"
            }
        }
```

**私有网络-VPN 网关**

```
"dimensions":{
    "unInstanceId":"vpngw-i0s10nr1",
    "objDetail":{         // 事件告警对象详情
        "VpnGatewayName":"vpn---fran",
        "InternetMaxBandwidthOut":"5Mps",
        "VpcName":"vy-vpn2",
        "VpcId":"vpc-709l0i0x"
            }
        }
```

##### 负载均衡-VIP 封堵

```
"dimensions":{
    "unInstanceId":"clb-test",
    "objDetail":{         // 事件告警对象详情
        "vip":"127.0.0.1"
            }
        }
```

**专线接入-物理专线**

```
"dimensions":{
            "objDetail":{
                "ar":"广州科学城",
                "bandwidth":"10000",
                "circuitNumber":"华新园0601-H0x-PL0x-x",
                "dcType":"裸光纤"
            },
            "unInstanceId":"dc-j0cp3tgr"
        }
```

**专线接入-专用通道**

```
"dimensions":{
            "objDetail":{
                "connLocalIp":"169.254.65.133",
                "connPeerIp":"169.254.65.134"
            },
            "unInstanceId":"dcx-881ekns2"
        }
```
