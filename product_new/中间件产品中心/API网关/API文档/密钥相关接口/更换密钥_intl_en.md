>!This is a legacy API which has been hidden and will no longer be updated. We recommend using the new [API Gateway API 3.0]( https://intl.cloud.tencent.com/document/product/628/36711) which is standardized and faster.
>
## API Description
This API (UpdateApiKey) is used to update a created API key pair.

## Input Parameters
The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/product/628/18814).

| Parameter Name | Required | Type | Description |
| -------- | ---- | ------ | --------- |
| secretID | Yes | String | secretID to be updated. |
| secretKey | No | String | secretKey to be updated, which is required when a custom key is updated. It can contain 10 to 50 letters, digits, and underscores. |

>`secretKey` should be entered when you update a custom key and can be ignored for automatically generated keys. If you want to create a custom key, please make sure that you are in the allowlist. You can contact your sales rep or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to be added to the allowlist.

## Output Parameters
| Parameter Name | Type | Description |
| ------------ | --------- | ---------------------------------------- |
| code | Int | Common error code. 0: success; other values: failure. For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/628/18822#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81). |
| codeDesc | String | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. |
| message | String | API-related module error message description. |
| secretID | String | secretID to be updated. |
| secretKey | String | secretKey after update. |
| type | String | Key type. |
| modifiedTime | Timestamp | Updated time in the format of YYYY-MM-DDThh:mm:ssZ according to ISO8601 standard. UTC time is used. |

## Samples
#### Sample 1
```
https://apigateway.api.qcloud.com/v2/index.php?
&<Common Request Parameter>
&Action=UpdateApiKey
&secretID=AKIDXXXXWKipDlK
```
Below is a sample return:
```
{
"code": "0",
"message": "",
"codeDesc": "Success",
"secretID": "AKIDXXXXWKipDlK",
"secretKey": "adasfdasffa",
"type": "auto",
"modifiedTime": "2017-08-07T00:00:00Z"
}
```

#### Sample 2
```
https://apigateway.api.qcloud.com/v2/index.php?
&<Common Request Parameter>
&Action=UpdateApiKey
&secretID=myTestsecretID
&secretKey= myTestSecretKey
```
Below is a sample return:
```
{
"code": "0",
"message": "",
"codeDesc": "Success",
"secretID": "myTestsecretID",
"secretKey": "myTestSecretKey",
"type": "manual",
"modifiedTime": "2017-08-07T00:00:00Z"
}
```
