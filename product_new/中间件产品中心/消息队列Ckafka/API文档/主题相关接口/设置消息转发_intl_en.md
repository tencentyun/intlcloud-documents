## 1. API Description
API domain name: `ckafka.api.qcloud.com`
This API (SetForward) is used to configure the forwarding rules for CKafka topics.



## 2. Input Parameters

The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/product/597/10084).

| Parameter Name | Required | Type | Description |
| --- | --- | --- | --- |
| instanceId | Yes | String | Instance ID |
| topicName | Yes | String | Topic name |
| status | Yes | Int | Forwarding task status. 0: add; 1: terminate |
| cosBucket | No | String | Forwarding cos bucket destination. Required if status is 0 |
| interval | No | Int | Forwarding time interval in seconds. Default value is 300 seconds. Maximum is 3,600 seconds. Minimum is 300 seconds |


## 3. Samples

Input:

```
 https://domain/v2/index.php?Action=SetForward&instanceId=ckafka-iamatest&topicName=mytopic&status=0&cosBucket=mybucket-125125125.cos.ap-guangzhou.myqcloud.com&interval=300<Common Request Parameters>
```

Output:

```
{
  "code": 0,
  "codeDesc": "Success",
  "message": "ok"
}

```

