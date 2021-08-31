## API Description
This API is used to replace the certificate used in a CLB instance.
 
Domain name for API calls: `lb.api.qcloud.com`


## Request Parameters

The list below contains only the API request parameters. Common parameters should be added when you call the API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/214/11594). The `Action` field for this API is `ReplaceCert`.
 
| Parameter | Required | Type | Description |
|----------------------|-----------------|------------------|-------------------|
| oldCertId | Yes | String | ID of the certificate to be replaced. This can be the ID of a server certificate, or a client certificate. |
| newCertId | No | String | ID of the new certificate. If this is left empty, the `newCertContent` and `newCertName` parameters are required. For a server certificate, the `newCertKey` parameter is also required. |
| newCertContent | No | String | Content of the new certificate. The `newCertId` parameter is required if this is left empty. |
| newCertName | No | String | Name of the new certificate. The `newCertId` parameter is required if this is left empty. |
| newCertKey | No | String | Private key of the new certificate. The `newCertId` parameter is required for a server certificate if this is left empty. |


## Response Parameters
 
 
| Parameter | Type | Description |
|-------|---|---------------|
| code | Int | Common error code. 0: success; other values: failure. For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/214/11602). |
| message | String | API-related module error message description. |
| codeDesc | String | Description of the task execution status. |

## Example
 
Request
<pre>
https://lb.api.qcloud.com/v2/index.php?Action=ReplaceCert
&<<a href="https://intl.cloud.tencent.com/document/product/213/31574">Common request parameters</a>>
&oldCertId=4b9fc92b
&newCertId=e2b6d555
</pre>
Response
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success"
}

```

 
