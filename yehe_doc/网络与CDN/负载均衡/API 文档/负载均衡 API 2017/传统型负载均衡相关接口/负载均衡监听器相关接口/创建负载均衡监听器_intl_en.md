## API Description
This API is used to create a CLB listener that provides the request forwarding rules, including parameters such as port, protocol, session persistence, and health check.

Domain name for API calls: `lb.api.qcloud.com`

The listener configuration rules are as follows:

- A CLB port can only have one protocol in the same CLB instance.
- Public network CLB listeners support HTTP, UDP, TCP, and HTTPS protocols, while private network CLB listeners only support UDP and TCP protocols.
- Batch creation is not supported when creating HTTPS listeners.


## Request Parameters
The list below contains only the API request parameters. Common parameters should be added when you call the API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/214/11594). The `Action` field for this API is `CreateLoadBalancerListeners`.


| Parameter | Required | Type | Description |
|-----------|--------|----------|----------|
| loadBalancerId | Yes | String | CLB instance ID, which can be queried via the <a href="https://intl.cloud.tencent.com/document/product/214/1261" title="DescribeLoadBalancers">DescribeLoadBalancers</a> API. |
| listeners.n.loadBalancerPort | Yes | Int | Listening port of the CLB listener. Valid range: 1-65535. `listeners` is an array. You can create n listeners, and `n` is a subscript. |
| listeners.n.instancePort | Yes | Int | Listening port of CLB listener’s real server. Value range: 1-65535. |
| listeners.n.protocol | Yes | Int | Protocol type of the CLB listener. 1: HTTP; 2: TCP; 3: UDP; 4: HTTPS.<br>Public network CLB listeners support HTTP, UDP, TCP and HTTPS protocols; <br>Private network CLB listeners only support TCP and UDP protocols. |
| listeners.n.listenerName | No | String | Name of the CLB listener. |
| listeners.n.sessionExpire | No | Int | Session persistence duration of the CLB listener. Value range: 0 or 30-3600. Default value: 0. |
| listeners.n.healthSwitch | No | Int | Whether to enable the health check for CLB listeners. 1: enable; 0: disable. Default value: 1. |
| listeners.n.timeOut | No | Int | Response timeout of health check for the CLB listener, in seconds. Valid range: 2-60, default value: 2.<br><font color="red">This parameter should be less than the check interval.</font><br>This parameter is currently unavailable to public network CLB listeners with HTTP or HTTPS protocol. |
| listeners.n.intervalTime | No | Int | Health check interval for the CLB listener, in seconds. Value range: 5-300. Default value: 5. |
| listeners.n.healthNum | No | Int | Healthy threshold of the CLB listener. Value range: 2-10. Default value: 3, indicating that if a forward is found healthy three consecutive times, it is considered to be normal. |
| llisteners.n.unhealthNum | No | Int | Unhealthy threshold of the CLB listener. Value range: 2-10. Default value: 3, indicating that if a forward is found unhealthy three consecutive times, it is considered to be abnormal. |
| listeners.n.httpHash | No | String | Forwarding method of the CLB listener. Only public CLB instances with HTTP or HTTPs listeners support this parameter. Valid values: wrr (weighted round robin), ip_hash (forwarding the hash of the source IP to the real server), least_conn (least connection).<br> Default value: wrr. |
| listeners.n.scheduler | No | String | Forwarding method of the CLB listener. Only public CLB instances with TCP or UDP listeners support this field. Valid values: wrr (weighted round robin), least_conn (least connection).<br> Default value: wrr. |
| listeners.n.httpCode | No | Int | Return code for health status of the HTTP or HTTPS listener of public network CLB instances. Valid range: 1-31. Default value: 31.<br>1 represents a return code of 1xx (healthy). 2 represents a return code of 2xx (healthy). 4 represents a return code of 3xx (healthy). 8 represents a return code of 4xx (healthy). 16 represents a return code of 5xx (healthy).<br>If there are multiple codes that can show the healthy status, enter the accumulated value corresponding to such codes. |
| listeners.n.httpCheckPath | No | String | Health check path for the HTTP or HTTPS listener of public network CLB instances. Default value: `/`. It must be started with `/` |
| listeners.n.SSLMode | No | String | SSL authentication type of the HTTPS listener of public network CLB instances. <br>unidirectional: one-way authentication; mutual: mutual authentication.<br><font color="red">This parameter is required to a HTTPS listener.</font>|
| listeners.n.certId | No | String | Server certificate ID. For HTTPS listeners, if this field is left empty, you must upload server certificate by specifying parameters including certContent, certKey, and certName. |
| listeners.n.certCaId | No | String | Client certificate ID. For HTTPS listeners, if `SSLMode=mutual` and this field is left empty, you must upload client certificate by specifying the certCaContent and certCaName parameters.|
| listeners.n.certCaContent | No | String | Content of the client certificate uploaded. For HTTPS listeners, if `SSLMode=mutual` and `certCaId` is left empty, this parameter must be passed in. |
| listeners.n.certCaName | No | String | Name of the client CA certificate uploaded. For HTTPS listeners, if `SSLMode=mutual` and `certCaId` is left empty, this parameter must be passed in. |
| listeners.n.certContent | No | String | Content of the server certificate uploaded. For HTTPS listeners, if `certId` is left empty, this parameter must be passed in. |
| listeners.n.certKey | No | String | Key of the server certificate uploaded. For HTTPS listeners, if `certId` is left empty, this parameter must be passed in. |
| listeners.n.certName | No | String | Name of the server certificate uploaded. For HTTPS listeners, if `certId` is left empty, this parameter must be passed in. |



## Response Parameters


| Parameter Name | Type | Description |
|-------|---|---------------|
| code | Int | Common error code. 0: success; other values: failure. For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/214/11602). |
| message | String | API-related module error message description. |
| codeDesc | String | Error code. For a successful operation, "Success" is returned. For a failed operation, a message describing the failure is returned. |
| requestId | Int | Request task ID. The operation status can be queried via the [DescribeLoadBalancersTaskResult](https://intl.cloud.tencent.com/document/product/214/4007) API.|
| listenerIds | Array | Listener ID array.|


## Example

Request
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=CreateLoadBalancerListeners
&<<a href="https://intl.cloud.tencent.com/document/product/213/31574">Common request parameters</a>>
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
Response
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

