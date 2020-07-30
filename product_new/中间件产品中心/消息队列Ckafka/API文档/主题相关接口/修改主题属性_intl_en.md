>!This is a legacy API which has been hidden and will no longer be updated. We recommend using the new [CKafka API 3.0](https://intl.cloud.tencent.com/document/product/597/36407) which is standardized and faster.
>
## 1. API Description
API domain name: `ckafka.api.qcloud.com`
This API (SetTopicAttributes) is used to modify the attributes of a topic on a CKafka instance.


## 2. Input Parameters

The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/product/597/10084).

| Parameter Name | Required | Type | Description |
| --- | --- | --- | --- |
| instanceId | Yes | String | Instance ID |
| topicName | Yes | String | Topic name |
| note| No | String | Topic remark should have no more than 64 characters. It must begin with a letter and can contain letters, digits and dashes (`-`) |
| enableWhiteList | No | Int | IP allowlist switch. 1: on; 0: off |
|minInsyncReplicas| No | Int | Default value is 1 |
|uncleanLeaderElectionEnable| No | Int | Default value is 0. 0: false; 1:true |
|retentionMs| No |Int | Message retention period. Unit: ms. Current minimum value is 60,000 ms |
|segmentMs | No |Int| Segment scrolling time. Unit: ms. Current minimum value is 86,400,000 ms |
|maxMessageBytes| No |Int| Maximum size of a topic message. Unit: bytes. Maximum value is 8,388,608 bytes, or 8 MB |


## 3. Samples

**Input:**

```http
 https://domain/v2/index.php?Action=SetTopicAttributes&instanceId=ckafka-xxxxxx&topicName=xxxxx&<Common Request Parameters>
```

**Output:**

```
{
"code": 0,
"codeDesc": "Success",
"message": "ok"
}
```
