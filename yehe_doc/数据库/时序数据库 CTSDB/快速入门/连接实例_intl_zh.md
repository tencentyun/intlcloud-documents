CTSDB 实例目前仅提供 VPC 网络下的连接方式。您可以通过控制台连接实例，也可以通过 RESTful API 接口连接实例，通过 API 接口连接实例时需要提供 root 帐号的密码，以确保安全性。

CURL 连接实例创建表的示例如下，其中`${user:password}`是实例的用户名和密码，`${vip}:${vport}`是实例的 IP 和 Port，`${metric_name}`是新建的表名称。参数介绍可参见 [新建 metric](https://intl.cloud.tencent.com/document/product/1100/40909)。
>?
>- 通过内网地址连接云数据库，[云服务器](https://intl.cloud.tencent.com/document/product/213/10517) 和数据库须是同一账号，且同一个[ VPC](https://intl.cloud.tencent.com/document/product/215/535) 内（保障同一个地域），或同在基础网络内。
>- 内网地址 IP 和 Port 可在 [控制台](https://console.cloud.tencent.com/ctsdb) 的实例列表查看。
>- 如忘记帐号密码，可参考 [重置密码](https://intl.cloud.tencent.com/document/product/1100/40920) 修改帐号密码。
>

```
   curl -u ${user:password} -H 'Content-Type:application/json' -X PUT ${vip}:${vport}/_metric/${metric_name} -d'
	 { 
	    "tags": {
	        "region": "string",
	        "set":  "long",
	        "host": "string"
	    },
	    "time": {
	         "name": "timestamp",
	         "format": "epoch_second"
	    },
	    "fields": {
	        "cpu_usage":  "float"
	    },
	    "options": {
	        "expire_day": 7,
	        "refresh_interval": "10s",
	        "number_of_shards": 5,
	        "number_of_replicas": 1,
	        "rolling_period": 1
	    }
	}'
```

