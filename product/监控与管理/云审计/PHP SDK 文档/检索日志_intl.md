
## SDK Description
LookupEvents is used to search for operation logs to allow users to query operation information.
## Request Parameters


| Parameter Name | Required | Type | Description |
|---------|---------|---------|--------|
| EndTime | Yes | DateTime | End time |
| LookupAttributes | Yes | Array | Array of attributes, which supports only one element. If it is not specified, the first ten entries are returned. |
| MaxResults | No | Number | Number of entries returned. If it is not specified, 10 entries are returned. A maximum 50 entries are supported. |
| NextToken | No | String | It is used when more logs are loaded. |
| StartTime | Yes | DateTime | Start time |
LookupAttributes is composed of the following parameters:
 
 | Parameter Name | Required | Type | Description |
|---------|---------|---------|--------|
| AttributeKey | No |	String | Search types (enumeration values), including Username (user name), EventName (event name), ResourceType (resource type), ResourceName (resource name), EventSource (event source), and EventId (Event ID). |
| AttributeValue | No |	String	| Value |
## Response Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| Events | Array | Array of events |
| NextToken | String | It is used when more logs are loaded. |

Events is composed of the following parameters:


| Parameter Name | Type | Description |
|---------|---------|---------|
| CloudAuditEvent | String | Event string |
| EventId | String | Event ID |
| EventName | String | Event name |
| EventSource | String | Event source |
| EventRegion | String | Region |
| EventTime | String | Event time |
| SecretId | String | Access key |
| EventRegion | String | Region |
| ErrorCode | Number | Error code. 0: normal; other error codes: error. |
| RequestID | String | Request ID |
| AccountID | String | ID of the primary account |
| SourceIPAddress | String | Source IP address |
| Resources | Object | Resource |
| Username | String | User name. Primary account: root; sub-account: sub-account ID; role user: roleUser. |

Resources is composed of the following parameters:

| Parameter Name | Type | Description |
|---------|---------|---------|
| ResourceName | String | Resource name |
| ResourceType | String |	Resource type |



## Example
### Request example

```
$config = array('SecretId'       => 'Your secretId',
                'SecretKey'      => 'Your secretKey',
                'RequestMethod'  => 'GET',
                'DefaultRegion'  => 'gz');
$ca = QcloudApi::load(QcloudApi::MODULE_CLOUDAUDIT, $config);
$nowTime = time();
$startTime = $nowTime-86400;
$package = array(
       'EndTime'=>$nowTime,
       'LookupAttributes'=>'[{"AttributeKey":"string","AttributeValue":"LookupEvents"}]',
       'MaxResults'=>10,
       'StartTime'=>$startTime
);
$a = $ca->LookUpEvents($package);
if ($a === false) {
    $error = $ca->getError();
    echo "Error code:" . $error->getCode() . ".\n";
    echo "message:" . $error->getMessage() . ".\n";
    echo "ext:" . var_export($error->getExt(), true) . ".\n";
} else {
    var_dump($a);
}
echo "\nRequest :" . $ca->getLastRequest();
echo "\nResponse :" . $ca->getLastResponse();
echo "\n";
```
### Response example

```
{
    "Events": [
        {
            "CloudAuditEvent": "{\"userIdentity\":{\"type\":\"Root\",\"principalId\":\"91000000009\",\"accountId\":\"91000000009\",\"userName\":\"root\",\"secretId\":\"AKIDVu8FBvowEONC2pw4RcbO2UnvsdDdvxqX\"},\"eventTime\":\"2017-11-02 19:08:14\",\"eventVersion\":\"1.0\",\"eventSource\":\"cloudaudit.api.tencentyun.com\\/v2\\/index.php\",\"requestParameters\":{\"Action\":\"LookupEvents\",\"EndTime\":\"1509620894\",\"LookupAttributes\":\"[{\\\"AttributeKey\\\":\\\"string\\\",\\\"AttributeValue\\\":\\\"LookupEvents\\\"}]\",\"MaxResults\":\"10\",\"Nonce\":\"24731\",\"Region\":\"ap-guangzhou\",\"RequestClient\":\"SDK_PHP_1.1\",\"SecretId\":\"AKIDVu8FBvowEONC2pw4RcbO2UnvsdDdvxqX\",\"SignatureMethod\":\"HmacSHA256\",\"StartTime\":\"1509534494\",\"Timestamp\":\"1509620894\",\"Version\":\"2017-03-12\"},\"sourceIPAddress\":\"10.251.88.12\",\"eventRegion\":\"ap-guangzhou\",\"eventName\":\"LookupEvents\",\"resourceType\":\"cloudaudit\",\"userAgent\":\"SDK_PHP_1.1\",\"errorCode\":\"0\",\"errorMessage\":\"end verify!permission verify\",\"requestID\":662138269,\"eventID\":\"5e9ec3fae7d93fd346cc28d397d4f1db1\",\"eventType\":\"ApiCall\",\"apiVersion\":\"2.0\",\"resources\":\"*\",\"resourceName\":\"*\"}",
            "EventId": "5e9ec3fae7d93fd346cc28d397d4f1db1",
            "EventName": "LookupEvents",
            "EventTime": "2017-11-02 19:08:14",
            "SecretId": "AKIDVu8FBvowEONC2pw4RcbO2UnvsdDdvxqX",
            "ErrorCode": "0",
            "RequestID": 662138269,
            "AccountID": "91000000009",
            "SourceIPAddress": "10.251.88.12",
            "EventSource": "cloudaudit.api.tencentyun.com/v2/index.php",
            "EventRegion": "ap-guangzhou",
            "Resources": {
                "ResourceName": "*",
                "ResourceType": "cloudaudit"
            },
            "Username": "root"
        },
        {
            "CloudAuditEvent": "{\"userIdentity\":{\"type\":\"Root\",\"principalId\":\"91000000009\",\"accountId\":\"91000000009\",\"userName\":\"root\",\"secretId\":\"AKIDPhngQxbmwzsYCkEJLCqKbloJhx4yoGhv\",\"sessionContext\":{\"token\":\"2226bb8e387f5aaa9a62c5db7f59f589ff871c131\",\"ua\":\"c3c4abeb0a8fb537b7dd9f07542b0758\",\"userIp\":\"14.17.22.36\",\"uin\":\"91000000009\",\"ownerUin\":\"91000000009\",\"appId\":\"1254962721\",\"expireTime\":\"2017-11-02 16:26:46\",\"mfa\":\"0\",\"mfaExpireTime\":\"2017-11-02 15:56:46\",\"interfaceName\":\"\",\"hasPolicyFilter\":\"0\",\"policyFilter\":\"\",\"extraInfo\":\"\"}},\"eventTime\":\"2017-11-02 15:56:53\",\"eventVersion\":\"1.0\",\"eventSource\":\"cloudaudit.api.tencentyun.com\\/v2\\/index.php\",\"requestParameters\":{\"Action\":\"LookupEvents\",\"EndTime\":\"1509638399\",\"MaxResults\":\"10\",\"Nonce\":\"12120\",\"Region\":\"gz\",\"RequestClient\":\"SDK_NODEJS_0.1.3\",\"RequestOperator\":\"91000000009\",\"RequestSource\":\"MC\",\"SecretId\":\"AKIDPhngQxbmwzsYCkEJLCqKbloJhx4yoGhv\",\"StartTime\":\"1509552000\",\"Timestamp\":\"1509609414\",\"Token\":\"2226bb8e387f5aaa9a62c5db7f59f589ff871c131\",\"seqId\":\"837e01d6-30c0-b943-d4fa-3c610323f619\",\"spanId\":\"https:\\/\\/console.cloud.tencent.com;35938\"},\"sourceIPAddress\":\"14.17.22.36\",\"eventRegion\":\"gz\",\"eventName\":\"LookupEvents\",\"resourceType\":\"cloudaudit\",\"userAgent\":\"SDK_NODEJS_0.1.3\",\"errorCode\":\"0\",\"errorMessage\":\"end verify!permission verify\",\"requestID\":1603560497,\"eventID\":\"7f59b78fec0ffe363b8cd30aad159cc31\",\"eventType\":\"ApiCall\",\"apiVersion\":\"2.0\",\"resources\":\"*\",\"resourceName\":\"*\"}",
            "EventId": "7f59b78fec0ffe363b8cd30aad159cc31",
            "EventName": "LookupEvents",
            "EventTime": "2017-11-02 15:56:53",
            "SecretId": "AKIDPhngQxbmwzsYCkEJLCqKbloJhx4yoGhv",
            "ErrorCode": "0",
            "RequestID": 1603560497,
            "AccountID": "91000000009",
            "SourceIPAddress": "14.17.22.36",
            "EventSource": "cloudaudit.api.tencentyun.com/v2/index.php",
            "EventRegion": "gz",
            "Resources": {
                "ResourceName": "*",
                "ResourceType": "cloudaudit"
            },
            "Username": "root"
        },
        {
            "CloudAuditEvent": "{\"userIdentity\":{\"type\":\"Root\",\"principalId\":\"91000000009\",\"accountId\":\"91000000009\",\"userName\":\"root\",\"secretId\":\"AKIDPhngQxbmwzsYCkEJLCqKbloJhx4yoGhv\",\"sessionContext\":{\"token\":\"2226bb8e387f5aaa9a62c5db7f59f589ff871c131\",\"ua\":\"c3c4abeb0a8fb537b7dd9f07542b0758\",\"userIp\":\"14.17.22.36\",\"uin\":\"91000000009\",\"ownerUin\":\"91000000009\",\"appId\":\"1254962721\",\"expireTime\":\"2017-11-02 16:26:46\",\"mfa\":\"0\",\"mfaExpireTime\":\"2017-11-02 15:56:46\",\"interfaceName\":\"\",\"hasPolicyFilter\":\"0\",\"policyFilter\":\"\",\"extraInfo\":\"\"}},\"eventTime\":\"2017-11-02 15:56:47\",\"eventVersion\":\"1.0\",\"eventSource\":\"cloudaudit.api.tencentyun.com\\/v2\\/index.php\",\"requestParameters\":{\"Action\":\"LookupEvents\",\"EndTime\":\"1509638399\",\"MaxResults\":\"10\",\"Nonce\":\"27974\",\"Region\":\"gz\",\"RequestClient\":\"SDK_NODEJS_0.1.3\",\"RequestOperator\":\"91000000009\",\"RequestSource\":\"MC\",\"SecretId\":\"AKIDPhngQxbmwzsYCkEJLCqKbloJhx4yoGhv\",\"StartTime\":\"1509552000\",\"Timestamp\":\"1509609407\",\"Token\":\"2226bb8e387f5aaa9a62c5db7f59f589ff871c131\",\"seqId\":\"d65a517d-c721-b139-2d1e-9bc88b5c7d4b\",\"spanId\":\"https:\\/\\/console.cloud.tencent.com;35978\"},\"sourceIPAddress\":\"14.17.22.36\",\"eventRegion\":\"gz\",\"eventName\":\"LookupEvents\",\"resourceType\":\"cloudaudit\",\"userAgent\":\"SDK_NODEJS_0.1.3\",\"errorCode\":\"0\",\"errorMessage\":\"end verify!permission verify\",\"requestID\":1352885274,\"eventID\":\"8311e673d12535f8a1ae66b163554c221\",\"eventType\":\"ApiCall\",\"apiVersion\":\"2.0\",\"resources\":\"*\",\"resourceName\":\"*\"}",
            "EventId": "8311e673d12535f8a1ae66b163554c221",
            "EventName": "LookupEvents",
            "EventTime": "2017-11-02 15:56:47",
            "SecretId": "AKIDPhngQxbmwzsYCkEJLCqKbloJhx4yoGhv",
            "ErrorCode": "0",
            "RequestID": 1352885274,
            "AccountID": "91000000009",
            "SourceIPAddress": "14.17.22.36",
            "EventSource": "cloudaudit.api.tencentyun.com/v2/index.php",
            "EventRegion": "gz",
            "Resources": {
                "ResourceName": "*",
                "ResourceType": "cloudaudit"
            },
            "Username": "root"
        },
        {
            "CloudAuditEvent": "{\"userIdentity\":{\"type\":\"Root\",\"principalId\":\"91000000009\",\"accountId\":\"91000000009\",\"userName\":\"root\",\"secretId\":\"AKIDVu8FBvowEONC2pw4RcbO2UnvsdDdvxqX\"},\"eventTime\":\"2017-11-02 15:06:41\",\"eventVersion\":\"1.0\",\"eventSource\":\"cloudaudit.api.cloud.tencent.com\\/v2\\/index.php\",\"requestParameters\":{\"Action\":\"LookupEvents\",\"EndTime\":\"1509606229\",\"LookupAttributes\":\"[{\\\"AttributeKey\\\":\\\"string\\\",\\\"AttributeValue\\\":\\\"\\\"}]\",\"MaxResults\":\"10\",\"Nonce\":\"39718\",\"Region\":\"gz\",\"RequestClient\":\"SDK_PHP_1.1\",\"SecretId\":\"AKIDVu8FBvowEONC2pw4RcbO2UnvsdDdvxqX\",\"StartTime\":\"1509519829\",\"Timestamp\":\"1509606229\"},\"sourceIPAddress\":\"14.17.22.36\",\"eventRegion\":\"gz\",\"eventName\":\"LookupEvents\",\"resourceType\":\"cloudaudit\",\"userAgent\":\"SDK_PHP_1.1\",\"errorCode\":\"0\",\"errorMessage\":\"end verify!permission verify\",\"requestID\":803010205,\"eventID\":\"cc737c139d689b109c265561a7e5bfe61\",\"eventType\":\"ApiCall\",\"apiVersion\":\"2.0\",\"resources\":\"*\",\"resourceName\":\"*\"}",
            "EventId": "cc737c139d689b109c265561a7e5bfe61",
            "EventName": "LookupEvents",
            "EventTime": "2017-11-02 15:06:41",
            "SecretId": "AKIDVu8FBvowEONC2pw4RcbO2UnvsdDdvxqX",
            "ErrorCode": "0",
            "RequestID": 803010205,
            "AccountID": "91000000009",
            "SourceIPAddress": "14.17.22.36",
            "EventSource": "cloudaudit.api.cloud.tencent.com/v2/index.php",
            "EventRegion": "gz",
            "Resources": {
                "ResourceName": "*",
                "ResourceType": "cloudaudit"
            },
            "Username": "root"
        }
    ],
    "NextToken": "MjAxNzExMDIxMywyMDE3MTEwMjEyLDIwMTcxMTAyMTEsMjAxNzExMDIxMCwyMDE3MTEwMjA5LDIwMTcxMTAyMDgsKzIwMTctMTEtMDIgMTk6MjM6MzQrMA==",
    "ListOver": false
}
```



