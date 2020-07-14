Your system can directly receive Tencent Cloud alarm notifications through the callback API. The callback API can push alarm notifications to URLs that are accessible over the public network through HTTP POST requests. You can take further actions based on the alarm notifications you receive from the callback API.

## Using the Callback API

- Callback API: you need to provide a URL that is able to receive HTTP POST requests and is accessible over the public network as the callback address.
- Callback trigger: the trigger logic is similar to that of alarm SMS and emails. When a created alarm policy is triggered or restored, an alarm notification will be sent through the callback API. Repeated alarms are also supported.
- Binding the callback API: you can configure a callback API by following step 8 of [Creating Alarm Policies](https://intl.cloud.tencent.com/document/product/248/6215) or add a callback API on the alarm policy details page. Only one alarm policy group can be bound to one alarm callback URL.
- Returned content: after an alarm notification is sent to the bound URL, we need to receive the following returned content to confirm that you have successfully received the notification. Otherwise, the same alarm notification will be sent to you repeatedly for up to three times.
  sessionId, which is used to authenticate the callback request.
  retCode, which is used to determine whether the request has been sent successfully.

```plaintext
{
	"sessionId": "xxxxxxxx",
	"retCode": 0
}
```

## Description of Callback API Parameters

The callback API will send data in JSON format through HTTP POST requests. The parameters are as follows:

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
            "dimensions": {               // The value of the `dimensions` field varies by product
                "unInstanceId": "ins-o9p3rg3m",  
                "objId":"xxxxxxxxxxxx"
            }
       },
       "alarmPolicyInfo": {
                "policyId": "policy-n4exeh88",   // ID of the alarm policy group
                "policyType": "cvm_device",     // Name of the alarm policy type
                "policyName": "test",      // Name of the alarm policy group
                "policyTypeCName": "CVM - basic monitoring",      // Displayed name of the alarm policy type
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
                    "alarmNotifyPeriod": 300                 // Frequency of repeated alarms in seconds (this field will not be returned for metrics without a threshold)
                }
        },
        "firstOccurTime": "2017-03-09 07:00:00",     // Time when the alarm is triggered for the first time
        "durationTime": 500,       // Alarm duration in seconds (if the alarm is unresolved, this value will be the duration from the time when the alarm is triggered for the first time to the time when the current alarm is sent)
        "recoverTime": "0"     // The time it takes to resolve the alarm in seconds (if the alarm is unresolved, the value of this parameter will be 0)
}
```

#### Sample metric alarm dimensions

##### Cloud Virtual Machine (CVM)

```
"dimensions": {
    "unInstanceId": "ins-xxxxxxxx",
    "objId": "94f1133c-46cf-4c61-a4c1-d928183aba47",       // Instance dimension bound to the backend
    "objName": "172.21.30.15#588789"       // Instance information returned in the alarm SMS message
}
```

##### CLB - public network listener

```
"dimensions": {
    "protocol": "https",
    "vip": "118.25.31.161",
    "vport": 443,
    "objId": "118.25.31.161#443#https",       // Instance dimension bound to the backend
    "objName": "CAuthCenteH5 | Classic network | 118.25.31.161(https:443)"       // Instance information returned in the alarm SMS message
}
```

##### CLB - private network listener

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
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
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
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

##### TencentDB for MySQL - master monitoring

```
"dimensions": {
    "uInstanceId": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

##### TencentDB for MySQL - slave monitoring

```
"dimensions": {
    "uInstanceId": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

##### TencentDB for Redis

```
"dimensions": {
    "redis_uuid": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

##### Direct Connect - connection

```
"dimensions": {
     "directconnectid": "xxx",
     "objId": "xxx",       // Instance dimension bound to the backend
     "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

##### Direct Connect - dedicated tunnel

```
"dimensions": {
    "directconnectconnid": "dcx-jizf8heu",
    "objId": "dcx-jizf8heu",       // Instance dimension bound to the backend
    "objName": "dcx-jizf8heu"       // Instance information returned in the alarm SMS message
}
```

##### VPC - direct connect gateway

```
"dimensions": {
    "directconnectgatewayid": "dcg-8wo1p2ve",
    "objId": "dcg-8wo1p2ve",       // Instance dimension bound to the backend
    "objName": "dcg-8wo1p2ve"       // Instance information returned in the alarm SMS message
}
```

##### Direct Connect - dedicated tunnel

```
"dimensions": {
    "directconnectconnid": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

##### VPC - NAT gateway

```
"dimensions": {
    "uniq_nat_id": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

##### VPC - VPN tunnel

```
"dimensions": {
    "vpnconnid": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

##### VPC - peering connection

```
"dimensions": {
    "peeringconnectionid": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

##### VPC - cross-region interconnection via the basic network

```
"dimensions": {
    "peeringconnectionid": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

##### VPC - direct connect gateway

```
"dimensions": {
    "directconnectgatewayid": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

##### VPC - VPN gateway

```
"dimensions": {
    "appid": 12345,
    "vip": "10.0.0.0",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

##### VPC - network detection

```
"dimensions": {
    "appid": 12345,
    "netdetectid": "xxx",
    "vpcid": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

##### VPC - shared bandwidth package

```
"dimensions": {
    "__region__": "xxx",
    "appid": 12345,
    "netgroup": "xxx",
    "objId": "xxx",       // Instance dimension bound to the backend
    "objName": "xxx"       // Instance information returned in the alarm SMS message
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
        "dimensions":{               // The value of the `dimensions` field varies by product
            "unInstanceId":"ins-pftdvqa2",
            "objDetail":{         // Details of the event alarm object
                "deviceLanIp":"172.21.0.17",
                "deviceWanIp":"118.89.233.99",
                "uniqVpcId":"vpc-ilrwkcbw"
            }
        }
    },
    "alarmPolicyInfo":{
        "policyId":"policy-n4exeh88",   // ID of the alarm policy group
        "policyType":"cvm_device",     // Name of the alarm policy type
        "policyName":"teset",      // Name of the alarm policy group
        "conditions":{
            "productName":"cvm",      // Name of the product type
            "productShowName":"CVM",      // Displayed name of the product type
            "eventName":"ping_unreachable",      // Event name
            "eventShowName":"ping unreachable",      // Event name
            "alarmNotifyType":"singleAlarm",    // Whether repeated alarms are supported ("singleAlarm": non-repeated alarm; "exponentialAlarm": exponential alarm; "continuousAlarm": persistent alarm. This field will not be returned for metrics without a threshold)
            "alarmNotifyPeriod":"0"                 // Frequency of repeated alarms in seconds (this field will not be returned for metrics without a threshold)
        },
        "policyTypeCName":"CVM - basic monitoring"      // Displayed name of the alarm policy type
    },
    "firstOccurTime":"2018-06-15 16:32:06",     // Time when the alarm is triggered for the first time
    "recoverTime":"0"      // The time it takes to resolve the alarm in seconds (if the alarm is unresolved or does not have a resolved status, the value of this parameter will be 0)
}
```

#### Sample event alarm dimensions

##### CVM

```
"dimensions":{
    "unInstanceId":"ins-pftdvqa2",
    "objDetail":{         // Details of the event alarm object
       "deviceLanIp":"172.21.0.17",
       "deviceWanIp":"118.89.233.99",
       "uniqVpcId":"vpc-ilrwkcbw"
            }
        }
```


##### TencentDB for MySQL

```
"dimensions": {
      "deviceName": "production-xd_item_center-0-offline-6035",
      "objDetail": {
        "IP": "10.80.17.217"
      },
      "unInstanceId": "cdb-bwieva60"
    }  
```



##### VPC - peering connection

```
"dimensions":{
    "unInstanceId":"pcx-142mpvfc",
    "objDetail":{         // Details of the event alarm object
        "PeeringConnectionName":"test-VPC1 <--> test-VPC3",
        "QosBandwidth":"100Mps",
        "VpcName":"test-VPC1",
        "VpcId":"vpc-5x1u9jq8"
            }
        }
```

##### VPC - VPN gateway

```
"dimensions":{
    "unInstanceId":"vpngw-i0s10nr1",
    "objDetail":{         // Details of the event alarm object
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
    "objDetail":{         // Details of the event alarm object
        "vip":"127.0.0.1"
            }
        }
```

##### Direct Connect - connection

```
"dimensions":{
            "objDetail":{
                "ar":"Guangzhou Science City",
                "bandwidth":"10000",
                "circuitNumber":"Huaxinyuan 0601-H04-PL01-1",
                "dcType":"Bare fiber"
            },
            "unInstanceId":"dc-j0cp3tgr"
        }
```

##### Direct Connect - dedicated tunnel

```
"dimensions":{
            "objDetail":{
                "connLocalIp":"169.254.65.133",
                "connPeerIp":"169.254.65.134"
            },
            "unInstanceId":"dcx-881ekns2"
        }
```
