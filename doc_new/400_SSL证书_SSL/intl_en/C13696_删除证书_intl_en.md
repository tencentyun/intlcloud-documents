## API Description
This API (CertDelete) is used to delete a certificate.
API request domain name: wss.api.qcloud.com

## Input Parameters
The list below contains only the API request parameters. The common request parameters need to be added when a call is made. For more information, see <a href="/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a>. The Action field of this API is CertDelete.

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| id | Yes | String | Certificate ID, which is the ID field in the list of certificates obtained from GetList |

## Output Parameters
| Parameter Name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code. 0: Successful; other values: Failed. For more information, see <a href="https://cloud.tencent.com/doc/api/372/%E9%94%99%E8%AF%AF%E7%A0%81#1.E3.80.81.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81" title="Common Error Codes">Common Error Codes</a> on the Error Codes page. |
| message | String | Module error message description depending on API. |
| codeDesc | String | Error code. For a successful operation, "Success" is returned. For a failed operation, a message describing the failure is returned. |

>! 
> - A free SSL certificate can be deleted only if its status is "review failed", "expired", or "revoked" or the verification fails 1 hour after the application.
> - A paid SSL certificate can be deleted only if its status is "expired" or "revoked".
> - SSL certificates associated with CLB, CDN, or BM cannot be deleted.
> - All managed SSL certificates except those associated with CLB, CDN, or BM can be deleted.

## Example
```
https://wss.test.api.qcloud.com/v2/index.php?
&<Common request parameters>
&Action=CertDelete
&id=xxxxxxxx
```
The returned results are as below:

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": []
}
```
