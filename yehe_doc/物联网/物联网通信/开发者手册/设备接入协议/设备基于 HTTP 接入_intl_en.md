## Parameter Description

When a device reports a message, it needs to carry `ProductId`, `DeviceName`, and `TopicName` to initiate an `http/https` request to the platform. The request API and parameters are as detailed below:

- Requested URL:
  ``
  https://ap-guangzhou.gateway.tencentdevices.com/device/publish
  ``
  ``
  http://ap-guangzhou.gateway.tencentdevices.com/device/publish
  ``

- Request method: POST

### Request parameters

| Parameter        | Required | Type    | Description                                                         |
| --------------- | ---- | ------- | ------------------------------------------------------------ |
| ProductId       | Yes   | String  | Product ID                                                     |
| DeviceName      | Yes   | String  | Device name                                                     |
| TopicName       | Yes   | String  | Name of the topic for publishing the message                                          |
| Payload         | Yes   | String  | Content of the published message                                               |
| PayloadEncoding | No   | String  | Encoding for the published message. Currently, only Base64-encoding is supported. If this parameter is left empty, the original message content will be sent. |
| Qos             | Yes   | Integer | Message QoS level                                                  |

>? The API only supports the `application/json` format.

### Signature generation

There are two types of signatures for request messages. Key authentication uses the HMACSHA256 algorithm, and certificate authentication uses the RSA_SHA256 algorithm. For more information, please see [Signature Algorithm](https://intl.cloud.tencent.com/document/product/1105/41501).

### Platform response parameters

| Parameter | Type | Description |
| --------- | ------ | ------ |
| RequestId | String | Request ID |

## Sample Code

#### Request packet

```
POST https://ap-guangzhou.gateway.tencentdevices.com/device/publish
Content-Type: application/json
Host: ap-guangzhou.gateway.tencentdevices.com
X-TC-Algorithm: HmacSha256
X-TC-Timestamp: 155****065
X-TC-Nonce: 5456
X-TC-Signature: 2230eefd229f582d8b1b891af7107b915972407****78ab3738f756258d7652c
{"DeviceName":"AAAAAA","Payload":"123","ProductId":"G8N****AHB","Qos":1,"TopicName":"G8N****AHB/AAAAAA/data"}
```

#### Response packet
<dx-codeblock>
:::  json
{
  "Response": {
    "RequestId": "f4da4f1f-d72e-40f1-****-349fc0072ba0"
  }
}
:::
</dx-codeblock>







