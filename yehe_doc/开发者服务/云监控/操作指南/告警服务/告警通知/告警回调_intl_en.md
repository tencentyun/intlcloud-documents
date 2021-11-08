Your WeCom group or self-built system can directly receive Cloud Monitor alarm notifications through API callback. API callback can push alarm notifications to URLs that are accessible over the public network through HTTP POST requests. You can take further actions based on the alarm notifications you receive from API callback. If you need to receive alarm notifications through a WeCom group, please see [Receiving Alarm Notifications Through a WeCom Group](https://intl.cloud.tencent.com/document/product/248/38208).

> ? 
> - Currently, alarm callback does not have an authentication mechanism and does not support HTTP authentication.
> - A failed alarm push can be retried up to three times, and each push request has a 5-second timeout period.
> - When an alarm policy created by the user is triggered or the alarm is resolved, the alarm messages will be pushed through the API callbacks. API callbacks also support repeated alarms.
> - The outbound IP of the Cloud Monitor callback API is dynamically and randomly allocated, so no specific IP information can be provided to you, but the IP port is fixed at 80. We recommend you configure a weighted opening policy in the security group based on port 80.
> - Alarm callback currently doesn't support pushing notifications by notification period. This will be supported in the future. Please stay tuned.
## Directions

1. Enter the [Notification Template](https://console.cloud.tencent.com/monitor/alarm2/notice) page in the Cloud Monitor console.
2. Click **Create** to create a notification template.
3. After configuring the basic information on the **Create Notification Template** page, enter a URL accessible over the public network as the callback API address (such as `domain name or IP[:port][/path]`) in the API callback module, and Cloud Monitor will push alarm messages to this address promptly.
4. Enter the [Alarm Policy List](https://console.cloud.tencent.com/monitor/alarm2/policy), click the name of the policy that needs to bind alarm callbacks to enter the alarm policy management page, and click the notification template.
5. Cloud Monitor will push the alarm messages through the HTTP POST requests to the URL of your system. You can further process the pushed alarm information by referring to [Alarm Callback Parameters](#.E5.91.8A.E8.AD.A6.E5.9B.9E.E8.B0.83.E5.8F.82.E6.95.B0.E8.AF.B4.E6.98.8E).
 ![](https://main.qcloudimg.com/raw/88ae443dd1118dd2939dda42928a8fcf.png)

## Alarm Callback Parameters

When an alarm rule is triggered, Cloud Monitor will send alarm messages to the URL of your system. The API callback sends data in the JSON format through the HTTP POST requests. You can further process the alarm information by referring to the following parameter descriptions.

### Metric alarm

#### Sample metric alarm parameters
>? The `durationTime` and `alarmStatus` values of most metrics are in the `string` data type.

```
{
       "sessionId": "xxxxxxxx",
       "alarmStatus": "1",    // 1: alarmed, 0: resolved
       "alarmType":"metric",    // Alarm type ("metric": metric alarm, "event": event alarm)
       "alarmObjInfo": {
            "region": "gz",  // This field will not be returned for services without the region attribute
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

> ? To get the policy type names and namespaces of a specific service, please see [Product Policy Type and Dimension Information](https://intl.cloud.tencent.com/document/product/248/39565).

#### Sample metric alarm dimensions

#### CVM - basic monitoring
```
"dimensions": {
		 "unInstanceId": "ins-aoaaah55", // CVM instance ID
		 "objId": "94f1133c-46cf-4c61-a4c1-d928183aba47",       // Instance dimension bound to the backend
		 "objName": "172.21.30.15#588789"       // Instance information returned in the alarm SMS message
}
```



#### CVM - storage monitoring
```
"dimensions": {
		 "diskid": "disk-1yukg09l", // Cloud disk ID
		 "objId": "disk-1yukg09l",       // Instance dimension bound to the backend
		 "objName": "disk-1yukg09l(Lstarsqlserverdb-011/ins-i7d3ifpp)"       // Instance information returned in the alarm SMS message
}
```




#### TencentDB for MySQL
```
"dimensions": {
		 "uInstanceId": "cdb-emzu6ysk",// TencentDB instance ID
		 "objId": "d6bc4b82-3acc-11eb-b11e-4cf95dd88ae6",       // Instance dimension bound to the backend
		 "objName": "cdb-emzu6ysk(instance name: platform development_xxljob,IP:10.66.234.242:3306)"       // Instance information returned in the alarm SMS message
}
```



#### TencentDB for Redis (1-minute)
```
"dimensions": {
		 "appid": "1252068037",    // Account `APPID`
		 "instanceid":"crs-1amp2588",  // TencentDB for Redis instance ID
		 "objId": "crs-af3bcreh",       // Instance dimension bound to the backend
		 "objName": "ID:crs-1amp2583|Instance Name:price|Ip Port:10.55.182.52:6379"       // Instance information returned in the alarm SMS message
}
```


#### TencentDB for Redis (5-second - Redis node)
```
"dimensions": {
		 "appid": "1252068000",    // Account `APPID`
		 "instanceid":"crs-1amp2588",  // TencentDB for Redis instance ID         
		 "rnodeid":"0f2ce0f969c4f43bc338bc1d6f60597d654bb3e4" // Redis node ID
		 "objId": "crs-1amp2588##2b6ff049e9845688f5150a9ee7fc8d38cab2222",       // Instance dimension bound to the backend 
		 "objName": "crs-1amp2588##2b6ff049e9845688f5150a9ee7fc8d38cab2222"       // Instance information returned in the alarm SMS message
}

```



#### TencentDB for Redis (5-second - instance summary)
```
"dimensions": {
		"AppId": "1252068000",    // Account `APPID`
		"InstanceId":"crs-1amp2588",  // TencentDB for Redis instance ID
		"objId": "crs-1amp288#[instancename]",       // Instance dimension bound to the backend
		"objName": "ID:crs-1amp288|Instance Name:price|Ip Port:10.99.182.52:9979"       //
		Instance information returned in the alarm SMS message
}
```



#### TencentDB for Redis (5-second - proxy node)
```
"dimensions": {
	   "appid": "1252068037",    // Account `APPID`
	   "instanceid":"crs-1amp2583",  // TencentDB for Redis instance ID
	   "pnodeid":"0f2ce0f969c4f43bc338bc1d6f60597d654bb3e4" // Proxy node ID
	   "objId": "crs-1amp2588##2b6ff049e9845688f5150a9ee7fc8d38cab222",       // Instance dimension bound to the backend
     "objName": "crs-1amp2588##2b6ff049e9845688f5150a9ee7fc8d38cab222"       // "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```



#### CLB - layer-7 protocol
```
"dimensions": {
		 "protocol": "https",    // Listener protocol
		 "vip": "14.22.4.26",  // CLB VIP
		 "port": "443",  // Real server port
		 "objId": "14.22.4.26#443#https",       // Instance dimension bound to the backend
		 "objName": "14.22.4.26#443#https"       // Instance information returned in the alarm SMS message
}
```



#### CLB - public network listener
```
"dimensions": {
		 "protocol": "https",   // Listener protocol
		 "vip": "118.25.31.161",   // CLB VIP
		 "vport": 443,  // Real server port
		 "objId": "118.25.31.161#443#https",       // Instance dimension bound to the backend (vip#vport#protocol)
		 "objName": "118.25.31.161#443#https"       // Instance information returned in the alarm SMS message (vip#vport#protocol)
}
```




#### CLB - private network listener
```
"dimensions": {
		 "protocol": "https",      // Listener protocol
		 "vip": "14.22.4.26",    // CLB VIP
		 "vpcId": vpc-1ywqac83,    // VPC ID
		 "vport": "443",          // Real server port
		 "objId": "14.22.4.26#443#https",       // Instance dimension bound to the backend (vip#vport#protocol)
		 "objName": "14.22.4.26#443#https"       // Instance information returned in the alarm SMS message (vip#vport#protocol)
}
```



#### CLB - server port (classic private network)
```
"dimensions": {
	   "protocol": "https",  // Listener protocol
		 "lanIp": "111.222.111.22",
		 "port": "440"  // Real server port
		 "vip": "14.12.13.25",  // CLB VIP
		 "vpcId": vpc-1ywqac83,   // VPC ID of CLB instance
		 "loadBalancerPort": "443",   // CLB listener port number
	 	 "objId": "14.12.13.25#443#https",       // Instance dimension bound to the backend
		 "objName": "14.12.13.25#443#https"       // Instance information returned in the alarm SMS message
}
```



#### TencentDB for SQL Server
```
"dimensions": {
		 "uid": "gamedb.gz18114.cdb.db",    
		 "objId": "mssql-nuvazldx(10.88.6.49:1433)",       // Instance dimension bound to the backend
		 "objName": "gamedb.gz18114.cdb.db"       // Instance information returned in the alarm SMS message
}
```



#### TencentDB for MongoDB
```
"dimensions": {
		"target": "cmgo-ajc6okuy",     
		"objId": "cmgo-ajc6okuy",       // Instance dimension bound to the backend
		"objName": "cmgo-ajc6okuy(instance name:bigdata_mongodb_big data,IP:10.1.1.23:27018)"       // Instance information returned in the alarm SMS message
}
```



#### TencentDB for PostgreSQL
```
"dimensions":{
     "uid":"2123"
     "objId":"2123",    // Instance dimension bound to the backend
     "objName":"ID:postgres-1292ja01|Instance Name:td100-dev-all-pgsql-1|Ip Port:10.80.24.3:5432"  // Instance information returned in the alarm SMS message
}
```


#### TDSQL-C
```
"dimensions":{
     "appid":"1256754779",
     "clusterid":"cynosdbmysql-p7ahy11x",
     "instanceid":"cynosdbmysql-inscyi56ruc",
     "insttype":"ro",
     "objId":"1256754779#cynosdbmysql-p7ahy11x#cynosdbmysql-ins-cyi56ruc#ro", // Instance dimension bound to the backend
     "objName":"1256754779#cynosdbmysql-p7ahy11x#cynosdbmysql-ins-cyi56ruc#ro" // Instance information returned in the alarm SMS message
}
```



#### TencentDB for TcaplusDB
```
"dimensions": {
     "ClusterId":"xxx",
     "TableInstanceId":"xxx",
		 "objId": "xxx",       // Instance dimension bound to the backend
     "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```


#### TDSQL for MySQL - instance summary
```
"dimensions": {
     "InstanceId":"tdsqlshard-jkeqopm0j",
     "objId": "xxx",       // Instance dimension bound to the backend
     "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```

#### TencentDB for MariaDB - instance summary
```
"dimensions": {
     "InstanceId":"tdsql-jkeqopm0j"
     "objId": "xxx",       // Instance dimension bound to the backend
     "objName": "xxx"       // Instance information returned in the alarm SMS message
	}
```

#### SCF
```
"dimensions": {
	   "appid": "1251316163",
     "function_name": "insert-tapd-task-result",  // Function name
     "namespace": "qmap-insight-core",  // SCF namespace
     "version": "$latest" ,    // Function version
		"objId": "1251316163#insert-tapd-task-result#qmap-insight-core#$latest",       // Instance dimension bound to the backend
		"objName": "1251316163#insert-tapd-task-result#qmap-insight-core#$latest"       // Instance information returned in the alarm SMS message
}
```



#### COS
```
"dimensions": {
		 "bucket": "fms-1255817900",       // Bucket name
		 "objId": "fms-1255817900",       // Instance dimension bound to the backend
		 "objName": "fms-1255817900"       // Instance information returned in the alarm SMS message
}
```



#### VPC - NAT gateway
```
"dimensions": {
		 "uniq_nat_id": "nat-4d545d",  // NAT gateway ID
		 "objId": "nat-4d545d",       // Instance dimension bound to the backend
		 "objName": "ID: nat-4d545d| Name: meeting access to information security NAT","uniq_nat_id":"nat-4d545d"     // Instance information returned in the alarm SMS message
}
```


#### VPC - VPN gateway
```
"dimensions": {
     "appid": "12345",
     "vip": "10.0.0.0",
     "objId": "xxx",       // Instance dimension bound to the backend
     "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```



#### VPC - VPN tunnel
```
"dimensions": {
     "vpnconnid": "vpnx-lr6cpqp6",
     "objId": "5642",       // Instance dimension bound to the backend
     "objName": "saicm-sit-to-office-td(China Telecom backup)(vpnx-lr6cpqp6)"       // Instance information returned in the alarm SMS message
}
```



#### VPC - Direct Connect gateway
```
"dimensions": {
     "directconnectgatewayid": "dcg-8wo1p2ve",
     "objId": "dcg-8wo1p2ve",       // Instance dimension bound to the backend
     "objName": "dcg-8wo1p2ve"       // Instance information returned in the alarm SMS message
}
```


#### VPC - peering connection
```
"dimensions": {
     "peeringconnectionid": "pcx-6gw5wy11",
     "objId": "pcx-6gw5wy11",       // Instance dimension bound to the backend
     "objName": "pcx-6gw5wy11"       // Instance information returned in the alarm SMS message
}
```


#### VPC - network detection
```
"dimensions":{
     "appid":"1258859999",
     "netdetectid":"netd-591p3g99",
		 "objId":"netd-591p3g99",  // Instance dimension bound to the backend
     "objName":"ID:netd-591p3g99|Name:check ad-185|Description:",   // Instance information returned in the alarm SMS message
     "vpcid":"vpc-mzfi69pi"
}
```



#### VPC - BWP
```
"dimensions": {
     "__region__": "xxx",
     "appid": 12345,
     "netgroup": "xxx",
     "objId": "xxx",       // Instance dimension bound to the backend
     "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```


#### CDN
```
"dimensions":{
     "appid":"1257137149",
     "domain":"cloud.tencent.com",
     "objId":"cloud.tencent.com",   // Instance dimension bound to the backend
     "objName":"cloud.tencent.com",  // Instance information returned in the alarm SMS message
     "projectid":"1174789"
}
```


#### CKafka - topic
```
"dimensions":{
     "appid":"1258399706",
     "instance_id":"ckafka-r7f1rrhh",
		 "topicid":"topic-cprg5vpp",
     "topicname":"topic-cluebaseserver-qb",
     "objId":"ckafka-r7f1rrhh",    // Instance dimension bound to the backend
     "objName":"ckafka-r7f1rrhh"     // Instance information returned in the alarm SMS message
}
```


#### CKafka - instance
```
"dimensions":{
     "appid":"1255817890",
     "instance_id":"ckafka-mdkk0kkk",
     "objId":"ckafka-mdkk0kkk",
     "objName":"ckafka-mdkk0kkk"
}
```


#### CKafka - consumer group - topic
```
"dimensions":{
     "appid":"1258344866",
     "consumer_group":"eslog-group22",
     "instance_id":"ckafka-65eago11",
		 "topicid":"topic-4q9jjy11",
     "topicname":"eslog"
     "objId":"1258344866#ckafka-65eago11#topic-4q9jjy11#eslog#eslog-group22",
     "objName":"125834866#ckafka-65eago11#topic-4q9jjy11#eslog#eslog-group22",
}
```



#### CKafka - consumer group - partition
```
"dimensions":{
     "appid":"1258344866",
     "consumer_group":"eslog-group22",
     "instance_id":"ckafka-65eago11",
		 "topicid":"topic-4q9jjy11",
     "topicname":"eslog",
		 "partition": "123456",
     "objId":"1258344866#ckafka-65eago11#topic-4q9jjy11#eslog#eslog-group22",
     "objName":"125834866#ckafka-65eago11#topic-4q9jjy11#eslog#eslog-group22",
}
```



#### CFS
```
"dimensions": {
		 "AppId": "1258638990", // Account `APPID`
		 "FileSystemId": "cfs-3e225da4p",     // File system ID
		 "objId": "cfs-3e225da4p",       // Instance dimension bound to the backend
		 "objName": "cfs-3e225da4p"       // Instance information returned in the alarm SMS message
}
```



#### Direct Connect - connection
```
"dimensions": {
     "directconnectid": "xxx",
     "objId": "xxx",       // Instance dimension bound to the backend
     "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```



#### Direct Connect - dedicated tunnel
```
"dimensions": {
     "directconnectconnid": "dcx-jizf8hrr",
     "objId": "dcx-jizf8hrr",       // Instance dimension bound to the backend
     "objName": "dcx-jizf8hrr"       // Instance information returned in the alarm SMS message
}
```

#### TKE (new) - container
```
"dimensions": {
     "objId": "xxx",       // Instance dimension bound to the backend
     "objName": "xxx",       // Instance information returned in the alarm SMS message
     "region":"xxx"
     "container_id":"xxx",
     "container_name":"xxx",
     "namespace":"xxx",
     "node":"xxx",
     "node_role":"xxx",
     "pod_name":"xxx",
     "tke_cluster_instance_id":"xxx",
     "un_instance_id":"xxx",
     "workload_kind":"xxx",
		 "workload_name":"xxx"
	}
```

#### TKE (new) - pod
```
"dimensions": {
     "objId": "xxx",       // Instance dimension bound to the backend
     "objName": "xxx",        // Instance information returned in the alarm SMS message
     "region":"xxx", 
     "namespace":"xxx",
     "node":"xxx",
     "node_role":"xxx",
     "pod_name":"xxx",
     "tke_cluster_instance_id":"xxx",
     "un_instance_id":"xxx",
     "workload_kind":"xxx",
		 "workload_name":"xxx"
	 }
```

#### TKE (new) - workload
```
"dimensions": {
     "objId": "xxx",       // Instance dimension bound to the backend
     "objName": "xxx",        // Instance information returned in the alarm SMS message
     "region":"xxx", 
     "namespace":"xxx",
     "tke_cluster_instance_id":"xxx",
     "workload_kind":"xxx",
		 "workload_name":"xxx"
	}
```

#### TKE (new) - workload
```
"dimensions": {
     "objId": "xxx",       // Instance dimension bound to the backend
     "objName": "xxx",       // Instance information returned in the alarm SMS message
     "region":"xxx", 
     "namespace":"xxx",
     "tke_cluster_instance_id":"xxx",
     "workload_kind":"xxx",
		 "workload_name":"xxx"
	}
```

#### TKE (new) - workload
```
"dimensions": {
     "objId": "xxx",       // Instance dimension bound to the backend
     "objName": "xxx",       // Instance information returned in the alarm SMS message
     "region":"xxx", 
     "node":"xxx",
		 "node_role":"xxx",
		 "pod_name":"xxx",
     "tke_cluster_instance_id":"xxx",
		 "un_instance_id":"xxx"
	}
```

#### TKE (new) - cluster component

```
"dimensions": {
     "objId": "xxx",       // Instance dimension bound to the backend
     "objName": "xxx",      // Instance information returned in the alarm SMS message
     "region":"xxx",
     "node":"xxx"
	}
```

#### TKE (new) - cluster
```
"dimensions": {
     "objId": "xxx",       // Instance dimension bound to the backend
     "objName": "xxx",       // Instance information returned in the alarm SMS message
     "region":"xxx",
     "tke_cluster_instance_id":"xxx"
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



#### CVM
```
"dimensions":{
     "unInstanceId":"ins-pftdvqa2",
		 "deviceName":"kube123",
     "objDetail":{         // Event alarm object details
         "deviceLanIp":"172.21.0.17",
         "deviceWanIp":"118.89.233.99",
         "uniqVpcId":"vpc-ilrwkcbw"
            }
        }
```





#### TencentDB for MySQL
```
"dimensions": {
      "deviceName": "production-xd_item_center-0-offline-6035",
      "objDetail": {
          "IP": "10.80.17.217"
      },
      "unInstanceId": "cdb-bwieva60"
    }  
```




#### VPC - peering connection

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




#### VPC - VPN gateway

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




#### Direct Connect - connection
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




#### Direct Connect - dedicated tunnel
```
"dimensions":{
            "objDetail":{
                "connLocalIp":"169.254.65.133",
                "connPeerIp":"169.254.65.134"
            },
            "unInstanceId":"dcx-881ekns2"
        }
```



