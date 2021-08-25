## Feature Overview

The device log feature is mainly used for the platform to remotely view the device operation logs. The platform can ask a device to report logs by sending a message. Log levels include ERROR, WARN, INFO, and DEBUG. The following two topics are needed for this feature:

- Data upstream topic (for publishing): `$log/operation/${productid}/${devicename}`
- Data downstream topic (for subscribing): `$log/operation/result/${productid}/${devicename}`

## Querying Log Level

1. The device sends a message in JSON format with the following content to the `$log/operation/${productid}/${devicename}` topic to query whether it should upload logs and the required log level:
```json
{
		"type": "get_log_level",
		"clientToken": "PPXLSKBUPZ-**"
}
```
2. The device actively queries whether it needs to report logs, or the platform remotely asks the device to enable log reporting. Specifically, the backend sends a message in JSON format with the following content to require log reporting and indicate the log level:
```
{
		"type": "get_log_level",
		"clientToken": "PPXLSKBUPZ-**",
		"log_level": 4,
		"result": 0,
		"timestamp": 1619599073
}
//log_level: 0: do not report logs; 1: ERROR; 2: WARN; 3: INFO; 4: DEBUG
```

## Log Upload

### Parameter description

When a device uploads logs, it needs to carry `ProductId` and `DeviceName` to initiate an `http/https` request to the platform. The request API and parameters are as detailed below:

- Requested URL:
 `http://ap-guangzhou.gateway.tencentdevices.com/device/reportlog`
 `https://ap-guangzhou.gateway.tencentdevices.com/device/reportlog`
- Request method: POST

### Request parameters

| Parameter | Required | Type | Description |
| ---------- | -------- | ------ | ------------------------------------------------------------ |
| ProductId | Yes | String | Product ID |
| DeviceName | Yes | String | Device name |
| Message | Yes | Array | Reported log content, which is a string array. The log level needs to be added before each log entry. Currently, DBG, INF, ERR, and WRN are supported |

>? The API only supports the `application/json` format.
>

### Signature generation

There are two types of signatures for request messages. Key authentication uses the HMACSHA256 algorithm, and certificate authentication uses the RSA_SHA256 algorithm. For more information, please see [Signature Algorithm](https://intl.cloud.tencent.com/document/product/1105/41501).

### Platform response parameters

| Parameter | Type | Description |
| --------- | ------ | ------ |
| RequestId | String | Request ID |


## Sample Code

#### Request packet

```
POST https://ap-guangzhou.gateway.tencentdevices.com/device/reportlog
Content-Type: application/json
Host: ap-guangzhou.gateway.tencentdevices.com
X-TC-Algorithm: HmacSha256
X-TC-Timestamp: 1551****65
X-TC-Nonce: 5456
X-TC-Signature: 2230eefd229f582d8b1b891af7107b91597240707d7****3738f756258d7652c
{"DeviceName":"AAAAAA","Message":["INFmqtt connect success."],"ProductId":"G8N9****HB"}
```

#### Response packet

```
{
		  "Response": {
			"RequestId": "f4da4f1f-d72e-40f1-****-349fc0072ba0"
		  }
}
```





