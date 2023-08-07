By using API callbacks, you can directly receive alarm notifications from Tencent Cloud Observability Platform (TCOP) on your WeCom group or self-built system. API callbacks can push alarm information to URLs that are accessible over the public network through HTTP POST requests. You can take further actions based on the alarm information pushed by API callbacks. If you need to receive alarm notifications through a WeCom group, see [Receiving Alarm Notifications through a WeCom Group](https://intl.cloud.tencent.com/document/product/248/38208).

> ? 
> - Currently, alarm callback does not have an authentication mechanism and does not support HTTP authentication.
> - A failed alarm push can be retried up to three times, and each push request has a 5-second timeout period.
> - When an alarm policy created by the user is triggered or the alarm is resolved, the alarm messages will be pushed through the API callbacks. API callbacks also support repeated alarms.
> - The outbound IP of the TCOP callback API is dynamically and randomly allocated, so no specific IP information can be provided to you, but the IP port is fixed at 80. We recommend you configure a weighted opening policy in the security group based on port 80.
> - Alarm callback currently doesn't support pushing notifications by notification period. This will be supported in the future. Please stay tuned.

## Directions

1. Enter the [TCOP Console — Notification Template](https://console.cloud.tencent.com/monitor/alarm2/notice) page.
2. Click **Create** to create a notification template.
3. After configuring the basic information on the **Create Notification Template** page, enter a URL accessible over the public network as the callback API address (such as `domain name or IP[:port][/path]`) in the API callback module, and TCOP will push alarm messages to this address promptly.
4. In the [Alarm Policy](https://console.cloud.tencent.com/monitor/alarm2/policy) list, click the name of an alarm policy to be associated with an alarm callback to enter the alarm policy management page. Select a notification template on the page that appears.
5. TCOP will push the alarm messages through the HTTP POST requests to the URL of your system. You can further process the pushed alarm information by referring to [Alarm Callback Parameters](#.E5.91.8A.E8.AD.A6.E5.9B.9E.E8.B0.83.E5.8F.82.E6.95.B0.E8.AF.B4.E6.98.8E).
 ![](https://main.qcloudimg.com/raw/88ae443dd1118dd2939dda42928a8fcf.png)

### Connecting to PagerDuty v2 through alarm callback

The following describes how to call back the alarm content to PagerDuty v2 through API callback:

Step 1: Enter a correct PagerDuty callback address. Currently, only PagerDuty v2 is supported. To avoid a callback failure, make sure the [callback address](https://events.pagerduty.com/v2/enqueue) is correct.

Step 2: After callback address is confirmed by the system, you need to enter a correct integration key in the input box below.

Step 3: Enter information for the **Notification Cycle** and **Notification Period** fields based on your business scenario.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/iH5F428_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16913987078000.png)


After the alarm callback is configured, you can receive the alarm callback information from TCOP when an alarm policy is triggered or when an alarm is resolved. Below is a sample:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/eeAH799_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_a61817b8-39bc-4e88-ab0c-1972ed976f4a.png)

### Alarm callback authentication
API callback supports the BasicAuth-based user security verification. If you want to send the alarm information callback to a service that requires the user’s verification, you can implement HTTP authentication in the API callback URL. For example, you can change `http://my.service.example.com` to `http://<USERNAME>:<PASSWORD>@my.service.example.com`.
![](https://qcloudimg.tencent-cloud.cn/raw/d35cb7693189e581fe9897656c46b31a.png)

## Alarm Callback Parameters

When an alarm rule is triggered, TCOP will send alarm messages to the URL of your system. The API callback sends JSON-formatted data through the HTTP POST requests. You can further process the alarm information by referring to the following parameter descriptions.

### Metric alarm

#### Sample metric alarm parameters
>?The data type of the `durationTime` and `alarmStatus` of most metrics is `string`, and the `namespace` of CVM’s network-related alarm metrics is `qce/lb`.

```
{
       "sessionId": "xxxxxxxx",
       "alarmStatus":"1",    // 1: Alerted, 0: Resolved
       "alarmType":"metric",    // Alarm type (`metric`: Metric alarm, `event`: Event alarm)
       "alarmObjInfo": {
            "region": "gz",  // This field will not be returned for products that are not region-specific
            "namespace": "qce/cvm",      // Product namespace
	        "appId": "xxxxxxxxxxxx",
            "uin": "xxxxxxxxxxxx",
            "dimensions": {               // Content in the `dimensions` field varies by service. For more information, see the sample metric alarm dimensions below
                "unInstanceId": "ins-o9p3rg3m",  
                "objId":"xxxxxxxxxxxx"
            }
       },
       "alarmPolicyInfo": {
                "policyId": "policy-n4exeh88",   // ID of the alarm policy group
                "policyType": "cvm_device",     // Alarm policy type name
                "policyName": "test",      // Name of the alarm policy group
                "policyTypeCName": "CVM - basic monitoring",      // Displayed name of the alarm policy type
                "conditions": {
                    "metricName": "cpu_usage",         // Metric name
                    "metricShowName": "CPU utilization",       // Displayed metric name
                    "calcType": ">",              // Comparison method (this field will not be returned for metrics without a threshold)
                    "calcValue": "90",            // Alarm threshold (this field will not be returned for metrics without a threshold)
					"calcUnit": "%",            // Unit of the alarm threshold (this field will not be returned for metrics without a threshold)
                    "currentValue": "100",       // Current alarm value (this field will not be returned for metrics without a threshold)
					"historyValue": "5",         //Historical alarm value (this field will not be returned for metrics without a threshold)
                    "unit": "%",                 // Unit (this field will not be returned for metrics without a threshold)
                    "period": "60",              // Statistical period in seconds (this field will not be returned for metrics without a threshold)
                    "periodNum": "1",            // Duration (this field will not be returned for metrics without a threshold)
                    "alarmNotifyType": "continuousAlarm",    // Whether repeated alarms are supported ("singleAlarm": Non-repeated alarm; "exponentialAlarm": Alarm repeated at exponential intervals; "continuousAlarm": Persistent alarm. This field will not be returned for metrics without a threshold)
                    "alarmNotifyPeriod": 300                 // Frequency of the repeated alarms in seconds (this field will not be returned for metrics without a threshold)
                }
        },
        "firstOccurTime": "2017-03-09 07:00:00",     // Time when the alarm is triggered for the first time
        "durationTime": 500,       // Alarm duration in seconds (if the alarm is unresolved, this value will be the duration from the time when the alarm is triggered for the first time to the time when the current alarm is sent)
        "recoverTime": "2017-03-09 07:50:00"     // Time when the alarm is resolved in seconds. If it is not resolved, the value is 0; if it is resolved, the specific time will be displayed, such as 2017-03-09 07:50:00.
}
```

> ? For product policy types and namespaces, see [Product Policy Type and Dimension Information](https://intl.cloud.tencent.com/document/product/248/39565) and [Tencent Cloud Service Metrics](https://www.tencentcloud.com/document/product/248/6140).

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
		 "uInstanceId": "cdb-emzu6ysk",// TencentDB for MySQL instance ID
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


#### TencentDB for Redis (5-second — Redis node)
```
"dimensions": {
		 "appid": "1252068000",    // Account `APPID`
		 "instanceid":"crs-1amp2588",  // TencentDB for Redis instance ID         
		 "rnodeid":"0f2ce0f969c4f43bc338bc1d6f60597d654bb3e4" // Redis node ID
		 "objId": "crs-1amp2588##2b6ff049e9845688f5150a9ee7fc8d38cab2222",       // Instance dimension bound to the backend 
		 "objName": "crs-1amp2588##2b6ff049e9845688f5150a9ee7fc8d38cab2222"       // Instance information returned in the alarm SMS message
}

```



#### TencentDB for Redis (5-second — instance summary)
```
"dimensions": {
		"AppId": "1252068000",    // Account `APPID`
		"InstanceId":"crs-1amp2588",  // TencentDB for Redis instance ID
		"objId": "crs-1amp288#[instancename]",       // Instance dimension bound to the backend
		"objName": "ID:crs-1amp288|Instance Name:price|Ip Port:10.99.182.52:9979"       // Alarm SMS message
		Instance information returned in the alarm SMS message
}
```



#### TencentDB for Redis (5-second — proxy node)
```
"dimensions": {
	   "appid": "1252068037",    // Account `APPID`
	   "instanceid":"crs-1amp2583",  // TencentDB for Redis instance ID
	   "pnodeid":"0f2ce0f969c4f43bc338bc1d6f60597d654bb3e4" // Proxy node ID
	   "objId": "crs-1amp2588##2b6ff049e9845688f5150a9ee7fc8d38cab222",       // Instance dimension bound to the backend
     "objName": "crs-1amp2588##2b6ff049e9845688f5150a9ee7fc8d38cab222"       // "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```



#### CLB — layer-7 protocol
```
"dimensions": {
         "protocol": "https",    // Listener protocol
         "vip": "14.22.4.26",  // CLB VIP
         "port": "443",  //Real server port
         "objId": "14.22.4.26#443#https",       // Instance dimension bound to the backend
         "objName": "clbtestname | Default-VPC | 18.25.31.161(htps:443) | service:clb, product:monitor"       // Alarm object information (namely `clbname`) returned in the alarm record | networkname | vip(protocol:vport) | tags
}
```


#### CLB — public network listener
```
"dimensions": {
         "protocol": "https",   // Listener protocol
         "vip": "118.25.31.161",   // CLB VIP
         "vport": 443,  // Real server port
         "objId": "118.25.31.161#443#https",       // Instance dimension bound to the backend (vip#vport#protocol)
         "objName": "clbtestname | Default-VPC | 18.25.31.161(htps:443) | service:clb, product:monitor"       // Alarm object information (namely `clbname`) returned in the alarm record | networkname | vip(protocol:vport) | tags
}
```




#### CLB — private network listener
```
"dimensions": {
         "protocol": "https",      // Listener protocol
         "vip": "14.22.4.26",    // CLB VIP
         "vpcId": vpc-1ywqac83,    // VPC ID
         "vport": "443",          // Real server port
         "objId": "14.22.4.26#443#https",       //   Instance dimension bound to the backend (vip#vport#protocol)
         "objName": "clbtestname | Default-VPC | 18.25.31.161(htps:443) | service:clb, product:monitor"       // Alarm object information (namely `clbname`) returned in the alarm record | networkname | vip(protocol:vport) | tags
}
```



#### CLB — server port (private network for Classic CLB)
```
"dimensions": {
	   "protocol": "https",  // Listener protocol
		 "lanIp": "111.222.111.22",
		 "port": "440"  //Real server port
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


#### TDSQL-C for MySQL
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
     "function_name": "insert-tapd-task-result",  // SCF function name
     "namespace": "qmap-insight-core",  // SCF namespace
     "version": "$latest" ,    // SCF version
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



##### VPC — NAT gateway
```
"dimensions": {
		 "uniq_nat_id": "nat-4d545d",  // NAT gateway ID
		 "objId": "nat-4d545d",       // Instance dimension bound to the backend
		 "objName": "ID: nat-4d545d| Name: meeting access to information security NAT","uniq_nat_id":"nat-4d545d"     // Instance information returned in the alarm SMS message
}
```


##### VPC — VPN gateway
```
"dimensions": {
     "appid": "12345",
     "vip": "10.0.0.0",
     "objId": "xxx",       // Instance dimension bound to the backend
     "objName": "xxx"       // Instance information returned in the alarm SMS message
}
```



#### VPC — VPN tunnel
```
"dimensions": {
     "vpnconnid": "vpnx-lr6cpqp6",
     "objId": "5642",       // Instance dimension bound to the backend
     "objName": "saicm-sit-to-office-td(China Telecom backup)(vpnx-lr6cpqp6)"       // Instance information returned in the alarm SMS message
}
```



#### VPC — direct connect gateway
```
"dimensions": {
     "directconnectgatewayid": "dcg-8wo1p2ve",
     "objId": "dcg-8wo1p2ve",       // Instance dimension bound to the backend
     "objName": "dcg-8wo1p2ve"       // Instance information returned in the alarm SMS message
}
```


#### VPC — peering connection
```
"dimensions": {
     "peeringconnectionid": "pcx-6gw5wy11",
     "objId": "pcx-6gw5wy11",       // Instance dimension bound to the backend
     "objName": "pcx-6gw5wy11"       // Instance information returned in the alarm SMS message
}
```


#### VPC — network detection
```
"dimensions":{
     "appid":"1258859999",
     "netdetectid":"netd-591p3g99",
		 "objId":"netd-591p3g99",  // Instance dimension bound to the backend
     "objName":"ID:netd-591p3g99|Name:check ad-185|Description:",   // Instance information returned in the alarm SMS message
     "vpcid":"vpc-mzfi69pi"
}
```



#### VPC — bandwidth package
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


#### CKafka — topic
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


#### CKafka — ConsumerGroup - topic
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



#### CKafka — ConsumerGroup - partition
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

#### TKE (metric v2.0) - container
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

#### TKE (metric v2.0) - pod
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

#### TKE (metric v2.0) - workload
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

#### TKE (metric v2.0) - workload
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

#### TKE (metric v2.0) - workload
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

#### TKE (metric v2.0) - cluster component

```
"dimensions": {
     "objId": "xxx",       // Instance dimension bound to the backend
     "objName": "xxx",      // Instance information returned in the alarm SMS message
     "region":"xxx",
     "node":"xxx"
	}
```

#### TKE (metric v2.0) - cluster
```
"dimensions": {
     "objId": "xxx",       // Instance dimension bound to the backend
     "objName": "xxx",       // Instance information returned in the alarm SMS message
     "region":"xxx",
     "tke_cluster_instance_id":"xxx"
	}
```
