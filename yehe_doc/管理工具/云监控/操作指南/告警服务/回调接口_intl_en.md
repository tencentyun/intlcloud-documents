
Your system can directly receive Tencent Cloud alarm notifications through the callback API. It can push alarm notifications to URLs accessible over the public network through HTTP POST requests. You can take further actions based on the received alarm notifications.


## Using callback API

- Callback API: you need to use a URL that can receive HTTP POST requests and can be accessed over the public network as the callback address.
- Callback trigger: the trigger logic is similar to that of alarm SMS and email. When a created alarm policy is triggered or resolved, an alarm notification will be sent through the callback API. Repeated alarms are also supported.
- Callback API binding: during step 3 (associating alarm recipient group) of alarm policy creation, you can click advanced configuration to configure the callback API, or add it on the alarm policy details page. One alarm policy group can be bound to only one alarm callback URL.
- Returned content: after an alarm notification is sent to the bound URL, we need to receive the following returned content to confirm that you have successfully received the notification. Otherwise, the same alarm notification will be sent to you repeatedly (for up to three times).
  `sessionId` is used to identify the callback request.
  `retCode` is used to determine whether the request is successfully sent.
```shell
{
	"sessionId": "xxxxxxxx",
	"retCode": 0
}
```

## Callback API parameter description

The callback API uses HTTP POST requests to send data in JSON format with the following parameters:
### Metric alarm
#### Sample metric alarm parameters
```
{
       "sessionId": "xxxxxxxx",
       "alarmStatus": 1,    // 1: alarmed, 0: resolved
       "alarmType":"metric",    // Alarm type ("metric": metric alarm, "event": event alarm)
       "alarmObjInfo": {
            "region": "gz",  // This field will not be returned for products that are not region-specific
            "namespace": "qce/cvm",      // Product namespace
            "dimensions": {               // Content in the `dimensions` field varies by product
                "unInstanceId": "ins-o9p3rg3m",  
                "objId":"xxxxxxxxxxxx"
            }
       },
       "alarmPolicyInfo": {
                "policyId": "policy-n4exeh88",   // Alarm policy group ID
                "policyType": "cvm_device",     // Alarm policy type name
                "policyName": "test",      // Alarm policy group name
                "policyTypeCName": "CVM - basic monitoring",      // Displayed name of alarm policy type
                "conditions": {
                    "metricName": "cpu_usage",         // Metric name
                    "metricShowName": "CPU utilization",       // Displayed metric name
                    "calcType": ">",              // Comparison method (this field will not be returned for metrics without a threshold)
                    "calcValue": "90",            // Alarm threshold (this field will not be returned for metrics without a threshold)
                    "currentValue": "100",       // Current alarm value (this field will not be returned for metrics without a threshold)
                    "unit": "%",                 // Unit (this field will not be returned for metrics without a threshold)
                    "period": "60",              // Statistical period in seconds (this field will not be returned for metrics without a threshold)
                    "periodNum": "1",            // Duration (this field will not be returned for metrics without a threshold)
                    "alarmNotifyType": "continuousAlarm",    // Whether repeated alarm is supported ("singleAlarm": non-repeated alarm; "exponentialAlarm": exponential alarm; "continuousAlarm": persistent alarm. This field will not be returned for metrics without a threshold)
                    "alarmNotifyPeriod": 300                 // Repeated alarm frequency in seconds (this field will not be returned for metrics without a threshold)
                }
        },
        "firstOccurTime": "2017-03-09 07:00:00",     // Time when the alarm is triggered for the first time
        "durationTime": 500,       // Alarm duration in seconds (if the alarm is not resolved, this value will be the duration between when the alarm is triggered for the first time and when the current alarm is sent)
        "recoverTime": "0"     // The time it takes to resolve the alarm in seconds (if the alarm is not resolved, this value will be 0)
}
```
#### Sample metric alarm dimensions
##### CVM
```
"dimensions": {
    "unInstanceId": "ins-xxxxxxxx",
    "objId": "94f1133c-46cf-4c61-a4c1-d928183aba47",       // Instance dimension bound to backend
    "objName": "172.21.30.15#588789"       // Instance information returned in alarm SMS
}
```

##### CLB - public network listener
```
"dimensions": {
    "protocol": "https",
    "vip": "118.25.31.161",
    "vport": 443,
    "objId": "118.25.31.161#443#https",       // Instance dimension bound to backend
    "objName": "CAuthCenteH5 | Basic network | 118.25.31.161(https:443)"       // Instance information returned in alarm SMS
}
```
##### CLB - private network listener
```
"dimensions": {
    "protocol": "",
    "vip": "",
    "vpcId": 123,
    "vport": "",
    "objId": "xxx",       // Instance dimension bound to backend
    "objName": "xxx"       // Instance information returned in alarm SMS
}
```

##### CLB - public network server port
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
    "objId": "xxx",       // Instance dimension bound to backend
    "objName": "xxx"       // Instance information returned in alarm SMS
}
```


##### CLB - private network server port
```
"dimensions": {
    "protocol": "",
    "lanIp": "",
    "port": "",
    "vip": "",
    "vpcId": 123,
    "loadBalancerPort": "",
    "objId": "xxx",       // Instance dimension bound to backend
    "objName": "xxx"       // Instance information returned in alarm SMS
}
```

##### TencentDB - MySQL - master monitoring
```
"dimensions": {
    "uInstanceId": "xxx",
    "objId": "xxx",       // Instance dimension bound to backend
    "objName": "xxx"       // Instance information returned in alarm SMS
}
```

##### TencentDB - MySQL - slave monitoring
```
"dimensions": {
    "uInstanceId": "xxx",
    "objId": "xxx",       // Instance dimension bound to backend
    "objName": "xxx"       // Instance information returned in alarm SMS
}
```

##### TencentDB - Redis
```
"dimensions": {
    "redis_uuid": "xxx",
    "objId": "xxx",       // Instance dimension bound to backend
    "objName": "xxx"       // Instance information returned in alarm SMS
}
```

##### Direct Connect - connection
```
"dimensions": {
     "directconnectid": "xxx",
     "objId": "xxx",       // Instance dimension bound to backend
     "objName": "xxx"       // Instance information returned in alarm SMS
}
```
##### Direct Connect - dedicated tunnel
```
"dimensions": {
    "directconnectconnid": "dcx-jizf8heu",
    "objId": "dcx-jizf8heu",       // Instance dimension bound to backend
    "objName": "dcx-jizf8heu"       // Instance information returned in alarm SMS
}
```
##### VPC - Direct Connect Gateway
```
"dimensions": {
    "directconnectgatewayid": "dcg-8wo1p2ve",
    "objId": "dcg-8wo1p2ve",       // Instance dimension bound to backend
    "objName": "dcg-8wo1p2ve"       // Instance information returned in alarm SMS
}
```

##### Direct Connect - dedicated tunnel
```
"dimensions": {
    "directconnectconnid": "xxx",
    "objId": "xxx",       // Instance dimension bound to backend
    "objName": "xxx"       // Instance information returned in alarm SMS
}
```

##### VPC - NAT Gateway
```
"dimensions": {
    "uniq_nat_id": "xxx",
    "objId": "xxx",       // Instance dimension bound to backend
    "objName": "xxx"       // Instance information returned in alarm SMS
}
```

##### VPC - VPN tunnel
```
"dimensions": {
    "vpnconnid": "xxx",
    "objId": "xxx",       // Instance dimension bound to backend
    "objName": "xxx"       // Instance information returned in alarm SMS
}
```

##### VPC - Peering Connection
```
"dimensions": {
    "peeringconnectionid": "xxx",
    "objId": "xxx",       // Instance dimension bound to backend
    "objName": "xxx"       // Instance information returned in alarm SMS
}
```

##### VPC - Classiclink
```
"dimensions": {
    "peeringconnectionid": "xxx",
    "objId": "xxx",       // Instance dimension bound to backend
    "objName": "xxx"       // Instance information returned in alarm SMS
}
```

##### VPC - Direct Connect Gateway
```
"dimensions": {
    "directconnectgatewayid": "xxx",
    "objId": "xxx",       // Instance dimension bound to backend
    "objName": "xxx"       // Instance information returned in alarm SMS
}
```

##### VPC - VPN Gateway
```
"dimensions": {
    "appid": 12345,
    "vip": "10.0.0.0",
    "objId": "xxx",       // Instance dimension bound to backend
    "objName": "xxx"       // Instance information returned in alarm SMS
}
```

##### VPC - network detection
```
"dimensions": {
    "appid": 12345,
    "netdetectid": "xxx",
    "vpcid": "xxx",
    "objId": "xxx",       // Instance dimension bound to backend
    "objName": "xxx"       // Instance information returned in alarm SMS
}
```

##### VPC - shared bandwidth package
```
"dimensions": {
    "__region__": "xxx",
    "appid": 12345,
    "netgroup": "xxx",
    "objId": "xxx",       // Instance dimension bound to backend
    "objName": "xxx"       // Instance information returned in alarm SMS
}
```

### Event alarm
#### Sample event alarm parameters
```
{
    "sessionId":"vuRH4ZlxBJSMNJHvNZhls9HY",
    "alarmStatus":"1",    // 1: alarmed, 0: resolved
    "alarmType":"event",    // Alarm type ("metric": metric alarm, "event": event alarm)
    "alarmObjInfo":{
        "region":"gz",      // This field will not be returned for products that are not region-specific
        "dimensions":{               // Content in the `dimensions` field varies by product
            "unInstanceId":"ins-pftdvqa2",
            "objDetail":{         // Event alarm object details
                "deviceLanIp":"172.21.0.17",
                "deviceWanIp":"118.89.233.99",
                "uniqVpcId":"vpc-ilrwkcbw"
            }
        }
    },
    "alarmPolicyInfo":{
        "policyId":"policy-n4exeh88",   // Alarm policy group ID
        "policyType":"cvm_device",     // Alarm policy type name
        "policyName":"teset",      // Alarm policy group name
        "conditions":{
            "productName":"cvm",      // Product type name
            "productShowName":"CVM",      // Displayed name of product type
            "eventName":"ping_unreachable",      // Event name
            "eventShowName":"ping unreachable",      // Event name
            "alarmNotifyType":"singleAlarm",    // Whether repeated alarm is supported ("singleAlarm": non-repeated alarm; "exponentialAlarm": exponential alarm; "continuousAlarm": persistent alarm. This field will not be returned for metrics without a threshold)
            "alarmNotifyPeriod":"0"                 // Repeated alarm frequency in seconds (this field will not be returned for metrics without a threshold)
        },
        "policyTypeCName":"CVM - basic monitoring"      // Displayed name of alarm policy type
    },
    "firstOccurTime":"2018-06-15 16:32:06",     // Time when the alarm is triggered for the first time
    "recoverTime":"0"      // The time it takes to resolve the alarm in seconds (if the alarm is unresolved or has no resolved status, this value will be 0)
}
```

#### Sample event alarm dimensions
##### CVM
```
"dimensions":{
    "unInstanceId":"ins-pftdvqa2",
    "objDetail":{         // Event alarm object details
       "deviceLanIp":"172.21.0.17",
       "deviceWanIp":"118.89.233.99",
       "uniqVpcId":"vpc-ilrwkcbw"
            }
        }
```
##### VPC - Peering Connection
```
"dimensions":{
    "unInstanceId":"pcx-142mpvfc",
    "objDetail":{         // Event alarm object details
        "PeeringConnectionName":"test-VPC1 <--> test-VPC3",
        "QosBandwidth":"100Mps",
        "VpcName":"test-VPC1",
        "VpcId":"vpc-5x1u9jq8"
            }
        }
```
##### VPC - VPN Gateway
```
"dimensions":{
    "unInstanceId":"vpngw-i0s10nr1",
    "objDetail":{         // Event alarm object details
        "VpnGatewayName":"vpn---fran",
        "InternetMaxBandwidthOut":"5Mps",
        "VpcName":"vy-vpn2",
        "VpcId":"vpc-709l0i0x"
            }
        }
```

##### CLB - VIP blocking
```
"dimensions":{
    "unInstanceId":"clb-test",
    "objDetail":{         // Event alarm object details
        "vip":"127.0.0.1"
            }
        }
```
