## 1. API Description
This API (CertDelete) is used to delete a certificate.
Domain name for API request: wss.api.qcloud.com

## 2. Input Parameters
The following request parameter list only provides the API request parameters. Common request parameters are required when the API is called. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/377/4153). The Action field for this API is CertDelete.

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| ID | Yes | String | Certificate ID, which is the ID field in the list of certificates obtained via GetList |

## 3. Output Parameters
| Parameter Name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code. 0: Successful; other values: Failed. |
| message | String | Module error message description depending on API |
| codeDesc | String | Error code. For a successful operation, "Success" is returned. For a failed operation, a message describing the failure is returned. |

>**Notes**:   

>1. A free SSL certificate can be deleted only when it is in "verification failed" status.
>2. A paid SSL certificate can be deleted only when it is in "verification canceled" or "verification failed" status.
>3. An SSL certificate associated with Cloud Load Balance cannot be deleted.
>4. An SSL certificate uploaded for hosting can be deleted in cases other than those mentioned above.
>

## 4. Example
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

