## 接口描述
CreateLoadBalancerListeners 接口提供了创建负载均衡监听器功能。负载均衡监听器提供了转发用户请求的具体规则，包括端口、协议、会话保持、健康检查等参数。
 
接口访问域名：`lb.api.qcloud.com`
 
监听器的配置规则如下：

- 在同一个负载均衡中，一个负载均衡端口只能对应一种协议，
- 支持 HTTP、UDP、TCP、HTTPS 协议，内网型只支持 UDP、TCP 协议，
- 当创建 HTTPS 协议监听器时，不支持批量创建。


## 请求参数
以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/product/214/11594) 页面。其中，此接口的 Action 字段为 CreateLoadBalancerListeners。


|参数名称|必选|类型|描述|
|-----------|--------|----------|----------|
|loadBalancerId|是|String|负载均衡实例 ID，可通过 <a href="https://intl.cloud.tencent.com/document/product/214/1261" title="DescribeLoadBalancers">DescribeLoadBalancers</a> 接口查询。|
|listeners.n.loadBalancerPort|是|Int|负载均衡监听器的监听接口，可选值：1~65535。listeners 为数组，可以创建多个监听器，n 为下标。|
|listeners.n.instancePort|是|Int|负载均衡实例监听器后端云服务器监听端口，可选值：1~65535。|
|listeners.n.protocol|是|Int|负载均衡实例监听器协议类型 1：HTTP，2：TCP，3：UDP，4：HTTPS。<br>公网属性负载均衡实例支持 HTTP、UDP、TCP、HTTPS 协议；<br>内网属性负载均衡实例支持 TCP 和 UDP 协议。|
|listeners.n.listenerName|否|String|负载均衡监听器的监听名称。|
|listeners.n.sessionExpire|否|Int|负载均衡监听器的会话保持时间，可选值：0或者30~3600，默认值0。|
|listeners.n.healthSwitch|否|Int|负载均衡实例监听器是否开启健康检查：1（开启）、0（关闭）。默认值 1，表示打开。|
|listeners.n.timeOut|否|Int|负载均衡监听器健康检查的响应超时时间，可选值：2-60，默认值：2，单位:秒。<br><font color="red">响应超时时间要小于检查间隔时间。</font><br>公网属性负载均衡 HTTP、HTTPS 协议的监听器响应超时时间暂不能设置。|
|listeners.n.intervalTime|否|Int|负载均衡监听器检查间隔时间，默认值5，可选值：5-300，单位：秒。|
|listeners.n.healthNum|否|Int|负载均衡监听器健康阈值，默认值3，表示当连续探测三次健康则表示该转发正常，可选值：2-10，单位：次。|
|listeners.n.unhealthNum|否|Int|负载均衡监听器不健康阈值，默认值3，表示当连续探测三次不健康则表示该转发不正常，可选值：2-10，单位：次。|
|listeners.n.httpHash|否|String|负载均衡监听器转发的方式。公网属性负载均衡（监听器为 HTTP、HTTPS）才支持此字段，可传值：wrr、ip_hash，least_conn<br>分别表示按权重轮询、根据源 IP 进行哈希出一个值转发到后端机器、最小连接数， 默认为 wrr。|
|listeners.n.scheduler|否|String|负载均衡监听器转发的方式。公网属性负载均衡（监听器为 TCP,UDP）才支持此字段，可传值：wrr、least_conn<br>分别表示按权重轮询、最小连接数， 默认为 wrr。|
|listeners.n.httpCode|否|Int|适用于公网属性负载均衡的 HTTP、HTTPS 协议的监听器，以该返回码来判断健康与否。可选值：1~31，默认31。<br>1代表返回值 `1xx` 表示健康，2代表返回 `2xx` 表示健康，4代表返回 `3xx` 表示健康，8代表返回 `4xx` 表示健康，16代表返回 `5xx` 表示健康。<br>若返回多种表示健康，则将相应的值累加。|
|listeners.n.httpCheckPath|否|String|适用于公网属性负载均衡的 HTTP、HTTPS 协议的监听器。默认 `/`，必须以 `/` 开头。|
|listeners.n.SSLMode|否|String|适用于公网属性负载均衡的 HTTPS 协议的监听器。<br>unidirectional：单向认证；mutual：双向认证。<br><font color="red"> HTTPS 协议监听器必选此项。</font>|
|listeners.n.certId|否|String|适用于公网属性负载均衡的 HTTPS 监听器。服务端证书的 ID，HTTPS 监听器如果不填写此项则必须上传证书，包括 certContent，certKey，certName|
|listeners.n.certCaId|否|String|适用于公网属性负载均衡的 HTTPS 监听器。客户端证书的 ID，如果SSLMode=mutual，HTTPS 监听器如果不填写此项则必须上传客户端证书，包括 certCaContent，certCaName|
|listeners.n.certCaContent|否|String|上传客户端证书的内容，HTTPS 监听器如果 SSLMode=mutual，如果没有 certCaId，则此项必传。|
|listeners.n.certCaName|否|String|上传客户端 CA 证书的名称，HTTPS 监听器如果 SSLMode=mutual，如果没有 certCaId，则此项必传。|
|listeners.n.certContent|否|String|上传服务端证书的内容，HTTPS 监听器如果没有 certId，则此项必传。|
|listeners.n.certKey|否|String|上传服务端证书的 key，HTTPS 监听器如果没有 certId，则此项必传。|
|listeners.n.certName|否|String|上传服务端证书的名称，HTTPS 监听器如果没有 certId，则此项必传。|



## 返回参数
 
 
|参数名称|类型|描述|
|-------|---|---------------|
|code|Int|公共错误码，0表示成功，其他值表示失败。详见错误码页面的 [公共错误码](https://intl.cloud.tencent.com/document/product/214/11602)。|
|message|String|模块错误信息描述，与接口相关。|
|codeDesc|String|英文错误码，成功返回 Success，失败有相应的英文说明。|
|requestId|Int|请求任务 ID，可根据 [DescribeLoadBalancersTaskResult](https://intl.cloud.tencent.com/document/product/214/4007) 接口查询操作状态。|
|listenerIds|Array|监听器 ID 的数组。|


## 示例
 
请求
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=CreateLoadBalancerListeners
&<<a href="https://intl.cloud.tencent.com/document/api/213/6976">公共请求参数</a>>
&loadBalancerId=lb-abcdefgh
&listeners.0.loadBalancerPort=443
&listeners.0.instancePort=443
&listeners.0.protocol=4
&listeners.0.SSLMode=mutual
&listeners.0.certName=myCertName
&listeners.0.certContent=-----BEGIN CERTIFICATE-----
			MIIE0DCCA7igAwIBAgIQEgaTYAJIpw1PQxjSr1FlTDANBgkqhkiG9w0BAQsFADBP
			MQswCQYDVQQGEwJDTjEaMBgGA1UEChMRV29TaWduIENBIExpbWl0ZWQxJDAiBgNV
			BAMMG0NBIOayg+mAmuWFjei0uVNTTOivgeS5piBHMjAeFw0xNjA1MTMwODIxMjVa
			Fw0xODA2MTMwODIxMjVaMBUxEzARBgNVBAMMCmcuZi14ai5jb20wggEiMA0GCSqG
			SIb3DQEBAQUAA4IBDwAwggEKAoIBAQC4/Ei7dxUJYXgY1V1PflCMwUrkG8Ack0vw
			+C/hCzivNBw5N0WA1Tch4REOIyDPIBq2wiblw4kSsHOF5CfB9DwDhaknZwzwyynZ
			Wr2NekKjoo6x0viqFydVyiVWGzW1qr6Dn9tiDcp75W/Os+nUzKHcc0Wd5aHvjGKD
			6xEPQKLvCZ0F4208rHWcoSnYiaFJPUAfegd8JvK5al0BvSZoXICo6Taf5x4xHag1
			6ymINH1ClLcAIOpAITWddqV20xaXrvdU7J0BusmYkHc840X3cvBywjFurzN5oLg2
			vtVQhGm6qJ/Fjqdg8w40BZkTQb4PlEX8AJ27g+548giuVnLzf8CHAgMBAAGjggHg
			MIIB3DAOBgNVHQ8BAf8EBAMCBaAwHQYDVR0lBBYwFAYIKwYBBQUHAwIGCCsGAQUF
			BwMBMAkGA1UdEwQCMAAwHQYDVR0OBBYEFBvlTUGHZ/GGU4qGT+T7r/Zbcg0pMB8G
			A1UdIwQYMBaAFDDadIbzKJBWntcxMcK9Wc2TEjkdMH8GCCsGAQUFBwEBBHMwcTA1
			BggrBgEFBQcwAYYpaHR0cDovL29jc3AyLndvc2lnbi5jbi9jYTJnMi9zZXJ2ZXIx
			L2ZyZWUwOAYIKwYBBQUHMAKGLGh0dHA6Ly9haWEyLndvc2lnbi5jbi9jYTJnMi5z
			ZXJ2ZXIxLmZyZWUuY2VyMD4GA1UdHwQ3MDUwM6AxoC+GLWh0dHA6Ly9jcmxzMi53
			b3NpZ24uY24vY2EyZzItc2VydmVyMS1mcmVlLmNybDBOBgNVHREERzBFggpnLmYt
			eGouY29tghBzY2hvbGFyLmYteGouY29tggt5dC5mLXhqLmNvbYILZmIuZi14ai5j
			b22CC3R3LmYteGouY29tME8GA1UdIARIMEYwCAYGZ4EMAQIBMDoGCysGAQQBgptR
			AQECMCswKQYIKwYBBQUHAgEWHWh0dHA6Ly93d3cud29zaWduLmNvbS9wb2xpY3kv
			MA0GCSqGSIb3DQEBCwUAA4IBAQCJSd/1xmxwnT/TtKvvxTvDnkCpfsFYVmqiHB/Z
			rXiMdgobUOfF7C8kcBCTqSQAXZF3fjJ1KyhNulvKOffzGGYp+rMwoTAmfaNLUxD/
			X9gPLxZCiysDBQ1BLe16k4aKUHIOmqQNF1MD/8hOZBxjevctKaXc4Xqm2gxJLxDH
			RoY3HKZcdB6t/x7YJU640wvaFqDqIgR6Pc74YjtLrNjkXcf/IQU7c2yjZt9NIGeS
			OTku5DmFasRf04tmE7naB+wkUZOwAqGK8CESNS11BYZjO/M4G/ALS8zCpShUy89H
			hYiYAG5jdNI4vyWwaU4428nG3YvKzlTOpCaowqgbyCcqmtAT
			-----END CERTIFICATE-----
&listeners.0.certKey=-----BEGIN RSA PRIVATE KEY-----
			your own key
			-----END RSA PRIVATE KEY-----
&listeners.0.certCaContent=-----BEGIN CERTIFICATE-----
			MIIEPDCCAySgAwIBAgIJAJiHd00fZNxoMA0GCSqGSIb3DQEBBQUAMHExCzAJBgNV
			BAYTAkNOMQswCQYDVQQIEwJHUzELMAkGA1UEBxMCU1oxDTALBgNVBAoTBFhYWFgx
			DjAMBgNVBAsTBVhYWFhYMQ4wDAYDVQQDEwVBQUFBQTEZMBcGCSqGSIb3DQEJARYK
			d3d3QHFxLmNvbTAeFw0xNjA4MTExMTUyNTZaFw0xNzA4MDIxMTUyNTZaMHExCzAJ
			BgNVBAYTAkNOMQswCQYDVQQIEwJHUzELMAkGA1UEBxMCU1oxDTALBgNVBAoTBFhY
			WFgxDjAMBgNVBAsTBVhYWFhYMQ4wDAYDVQQDEwVBQUFBQTEZMBcGCSqGSIb3DQEJ
			ARYKd3d3QHFxLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAM29
			SL0TlZaqZb4jEjZ8mkwSeWGVhYaskYtDvxvZQSHZF2A1DtpGojsz+Z3KxgVo4edj
			Y26lfxmFPwPhxoBRgCYDqEOLAOKWRxzXYyP2kr9FN4vs0hzizT4IVxJciOUwmIaQ
			bjzzFQN5BeJ/UTekrs1/YwfJAakP7TvoKUlfBvkKFzRlgdxnGk+/C7+cg1P9F9J4
			rjm/Rn+0HhO0QshsAo1IT4jZF356yvk/g0upLhZexo39jKf4ypmtcHTusYcAoRGh
			bCk26taM4aeQxMnB715ZkQhqB1+dyM6SWRFysYpteEK+jEH8wWPQriqIlcRJxncy
			/8B4RmHIJxXRG8Tb8TUCAwEAAaOB1jCB0zAdBgNVHQ4EFgQUp/qOq6q7ezAVxEhX
			trsPMa4aiq4wgaMGA1UdIwSBmzCBmIAUp/qOq6q7ezAVxEhXtrsPMa4aiq6hdaRz
			MHExCzAJBgNVBAYTAkNOMQswCQYDVQQIEwJHUzELMAkGA1UEBxMCU1oxDTALBgNV
			BAoTBFhYWFgxDjAMBgNVBAsTBVhYWFhYMQ4wDAYDVQQDEwVBQUFBQTEZMBcGCSqG
			SIb3DQEJARYKd3d3QHFxLmNvbYIJAJiHd00fZNxoMAwGA1UdEwQFMAMBAf8wDQYJ
			KoZIhvcNAQEFBQADggEBAJ2XTOKyR2nFgaWcTG5d92tSij3lIoZCBo4dwrleYFuW
			cYUYSi65QskJpuDHr5KttmI4+0tt9OQOB/oHIEbkCqgEAC7PREJAgapcf5+ItMHN
			rNh151CkTyoK1Z09tw3OrX5GQVAHSpz0+BQTE+MPas5lyidwP1PqQFY9nZW4J3PG
			RAbiiSnQ1eN5g0aKzIZpbEbP7Y7BGT9b+rLt+VUbmQ30h96zHchSsUsQ32dchwLm
			N0ZL1PyCivQ+A1snbqA3uHZnoXBd8/yq0QNg0o15edx+GfbY5FJbgXf3FER+NgMB
			wPeJ62izpROBQvXYNb3e72gM1xCAlgD+MBpNeGlx56g=
			-----END CERTIFICATE-----
&listeners.0.certCaName=myCertCaName
</pre>
返回
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "requestId": 28557,
    "listenerIds": [
        "lbl-hox8i4q0"
    ]
}
```
 
