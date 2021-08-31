Your WeCom group or self-built system can directly receive Cloud Monitor alarm notifications through API callback. API callback can push alarm notifications to URLs that are accessible over the public network through HTTP POST requests. You can take further actions based on the alarm notifications you receive from API callback.

> ? 
> - After you save the callback URL, the system will automatically verify your URL once. The timeout threshold for this verification is 5 seconds. When an alarm policy created by the user is triggered or the alarm is resolved, the alarm messages will be pushed through the API callbacks. An alarm message can be pushed up to three times, and the timeout threshold for each request is 5 seconds.
> - When an alarm policy created by the user is triggered or the alarm is resolved, the alarm messages will be pushed through the API callbacks. API callbacks also support repeated alarms.
> - The outbound IP of the Cloud Monitor callback API is dynamically and randomly allocated, so no specific IP information can be provided to you, but the IP port is fixed at 80. We recommend you configure a weighted opening policy in the security group based on port 80.

## Directions

1. Enter the [Notification Template](https://console.cloud.tencent.com/monitor/alarm2/notice) page in the Cloud Monitor console.
2. Click **Create** to create a notification template.
3. After configuring the basic information on the notification template creation page, enter an alarm callback URL accessible over the public network in the API callback module.
4. Enter the [Alarm Policy List](https://console.cloud.tencent.com/monitor/alarm2/policy), click the name of the policy that needs to bind alarm callbacks to enter the alarm policy management page, and click the notification template.
5. If the HTTP response returns code 200, the verification is successful. After the callback URL is successfully verified, Cloud Monitor will push the alarm messages through the HTTP POST requests to the URL of your system. You can further process the pushed alarm information by referring to [Alarm Callback Parameters](#.E5.91.8A.E8.AD.A6.E5.9B.9E.E8.B0.83.E5.8F.82.E6.95.B0.E8.AF.B4.E6.98.8E).
   ![](https://main.qcloudimg.com/raw/88ae443dd1118dd2939dda42928a8fcf.png)

## Alarm Callback Parameters

When an alarm rule is triggered, Cloud Monitor will send alarm messages to the URL of your system. The API callback sends data in the JSON format through the HTTP POST requests. You can further process the alarm information by referring to the following parameter descriptions.

### Metric alarm

#### Sample metric alarm parameters

```
{
       "sessionId": "xxxxxxxx",
       "alarmStatus": 1,    // 1: alarmed, 0: resolved
       "alarmType":"metric",    // Alarm type ("metric": metric alarm, "event": event alarm)
       "alarmObjInfo": {
            "region": "gz",  // This field will not be returned for services that are not region-specific
            "namespace": "qce/cvm",      // Service namespace
            "dimensions": {               // Content in the `dimensions` field varies by service. For more information, please see the sample metric alarm dimensions below
                "unInstanceId": "ins-o9p3rg3m",  
                "objId":"xxxxxxxxxxxx"
            }
       },
       "alarmPolicyInfo": {
                "policyId": "policy-n4exeh88",   // Alarm policy group ID
                "policyType": "cvm_device",     // Alarm policy group name
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
                    "alarmNotifyType": "continuousAlarm",    // Whether repeated alarms are supported ("singleAlarm": non-repeated alarm; "exponentialAlarm": exponential alarm; "continuousAlarm": persistent alarm. This field will not be returned for metrics without a threshold)
                    "alarmNotifyPeriod": 300                 // Frequency of the repeated alarms in seconds (this field will not be returned for metrics without a threshold)
                }
        },
        "firstOccurTime": "2017-03-09 07:00:00",     // Time when the alarm is triggered for the first time
        "durationTime": 500,       // Alarm duration in seconds (if the alarm is unresolved, this value will be the duration from the time when the alarm is triggered for the first time to the time when the current alarm is sent)
        "recoverTime": "0"     // The time it takes to resolve the alarm in seconds (if the alarm is unresolved, the value of this parameter will be 0)
}
```

> ? 
> - To get the namespace and metric names of a specific service, please see [Tencent Cloud Service Metrics](https://intl.cloud.tencent.com/document/product/248/6843).
> - To get the policy type names of a specific service, please see Tencent Cloud Service Policy Type.

#### Sample metric alarm dimensions

**CVM**

```
"dimensions": {
    "unInstanceId": "ins-xxxxxxxx",
    "objId": "94f1133c-46cf-4c61-a4c1-d928183aba47",       // Instance dimension bound to the backend
    "objName": "172.21.30.15#588789"       // Instance information returned in the alarm SMS message
}
```

**CLB - public network listener**

```
"dimensions": {
    "protocol": "https",
    "vip": "118.25.31.161",
    "vport": 443,
    "objId": "118.25.31.161#443#https",       // Instance dimension bound to the backend
    "objName": "CAuthCenteH5 | Classic network | 118.25.31.161(https:443)"       // Instance information returned in the alarm SMS message
}
```

**CLB - private network listener**

```
"dimensions": {
    "protocol": "",
    "vip": "",
    "vpcId": 123,
    "vport": "",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

**CLB - public network server port**

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
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

**CLB - private network server port**

```
"dimensions": {
    "protocol": "",
    "lanIp": "",
    "port": "",
    "vip": "",
    "vpcId": 123,
    "loadBalancerPort": "",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

**TencentDB for MySQL - primary monitoring**

```
"dimensions": {
    "uInstanceId": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

**TencentDB for MySQL - secondary monitoring**

```
"dimensions": {
    "uInstanceId": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

**TencentDB for Redis**

```
"dimensions": {
    "redis_uuid": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

**Direct Connect - connection**

```
"dimensions": {
     "directconnectid": "xxx",
     "objId": "xxx",       // Instance dimension bound to the backend
     "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

**Direct Connect - dedicated tunnel**

```
"dimensions": {
    "directconnectconnid": "dcx-jizf8heu",
    "objId": "dcx-jizf8heu",       // Instance dimension bound to the backend
    "objName": "dcx-jizf8heu"       // Instance information returned in the alarm SMS message
}
```

**VPC - Direct Connect gateway**

```
"dimensions": {
    "directconnectgatewayid": "dcg-8wo1p2ve",
    "objId": "dcg-8wo1p2ve",       // Instance dimension bound to the backend
    "objName": "dcg-8wo1p2ve"       // Instance information returned in the alarm SMS message
}
```

**Direct Connect - dedicated tunnel**

```
"dimensions": {
    "directconnectconnid": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

**VPC - NAT gateway**

```
"dimensions": {
    "uniq_nat_id": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

**VPC - VPN tunnel**

```
"dimensions": {
    "vpnconnid": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

**VPC - peering connection**

```
"dimensions": {
    "peeringconnectionid": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

**VPC - cross-region interconnection over the classic network**

```
"dimensions": {
    "peeringconnectionid": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

**VPC - Direct Connect Gateway**

```
"dimensions": {
    "directconnectgatewayid": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

**VPC - VPN gateway**

```
"dimensions": {
    "appid": 12345,
    "vip": "10.0.0.0",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

**VPC - network detection**

```
"dimensions": {
    "appid": 12345,
    "netdetectid": "xxx",
    "vpcid": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

**VPC - shared bandwidth package**

```
"dimensions": {
    "__region__": "xxx",
    "appid": 12345,
    "netgroup": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

**CDN**

```
"dimensions":{
    "appid":"xxx",
    "domain":"xxx",
    "objId":"xxx",
    "objName":"xxx",
    "projectid":"xxx"
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
        "region":"gz",      // This field will not be returned for services that are not region-specific
        "dimensions":{               // The value of the `dimensions` field varies by service
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
        "policyType":"cvm_device",     // Alarm policy group name
        "policyName":"teset",      // Alarm policy group name
        "conditions":{
            "productName":"cvm",      // Service name
            "productShowName":"CVM",      // Displayed service name
            "eventName":"ping_unreachable",      // Event name
            "eventShowName":"ping unreachable",      // Event name
            "alarmNotifyType":"singleAlarm",    // Whether repeated alarms are supported ("singleAlarm": non-repeated alarm; "exponentialAlarm": exponential alarm; "continuousAlarm": persistent alarm. This field will not be returned for metrics without a threshold)
            "alarmNotifyPeriod":"0"                 // Frequency of the repeated alarms in seconds (this field will not be returned for metrics without a threshold)
        },
        "policyTypeCName":"CVM - basic monitoring"      // Displayed name of alarm policy type
    },
    "firstOccurTime":"2018-06-15 16:32:06",     // Time when the alarm is triggered for the first time
    "recoverTime":"0"      // The time it takes to resolve the alarm in seconds (if the alarm is unresolved or does not have a resolved status, the value of this parameter will be 0)
}
```

#### Sample event alarm dimensions

**CVM**

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

**TencentDB for MySQL**

```
"dimensions": {
      "deviceName": "production-xd_item_center-0-offline-6035",
      "objDetail": {
        "IP": "10.80.17.217"
      },
      "unInstanceId": "cdb-bwieva60"
    }  
```

**VPC - peering connection**

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

**VPC - VPN gateway**

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

#### CLB - VIP blocking

```
"dimensions":{
    "unInstanceId":"clb-test",
    "objDetail":{         // Event alarm object details
        "vip":"127.0.0.1"
            }
        }
```

**Direct Connect - connection**

```
"dimensions":{
            "objDetail":{
                "ar":"Guangzhou Science City",
                "bandwidth":"10000",
                "circuitNumber":"Huaxinyuan 0601-H0x-PL0x-x",
                "dcType":"Bare fiber"
            },
            "unInstanceId":"dc-j0cp3tgr"
        }
```

**Direct Connect - dedicated tunnel**

```
"dimensions":{
            "objDetail":{
                "connLocalIp":"169.254.65.133",
                "connPeerIp":"169.254.65.134"
            },
            "unInstanceId":"dcx-881ekns2"
        }
```
