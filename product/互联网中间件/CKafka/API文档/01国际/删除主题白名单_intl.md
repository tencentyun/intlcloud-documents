>!This is a legacy API which has been hidden and will no longer be updated. We recommend using the new [CKafka API 3.0](https://intl.cloud.tencent.com/document/product/597/36407) which is standardized and faster.
>
## 1. API Description

This API (DeleteTopicIpwhitelist) is used to delete the allowlist of a topic.

Domain name for API request: ckafka.api.qcloud.com

## 2. Input Parameters

The following request parameter list only provides API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/431/5883).

| Parameter Name | Required | Type | Description |
| --- | --- | --- | --- |
| instanceId | Yes | String | Instance ID |
| topicName | Yes | String | Topic name |
| Ip.n | Yes | String | Required. IP allowlist |

## 3. Example

Input:

```
 https://domain/v2/index.php?Action=DeleteTopicIpwhitelist&instanceId=ckafka-xxooa0&topicName=tinatest&ip.n=111.111.111.11&<Common request parameters>
```

Output:

```
  {
      "code" : 0,
"codeDesc":"Success"
      "message" : "ok",
  }

```
> Note: This API deletes the IPs in ipWhiteList from the existing allowlist.
