### API Description
This API (AssumeRoleWithSAML) is used to request temporary credentials for a role based on SAML assertion.
Request domain name: sts.api.qcloud.com
Request method: HTTP POST

### Input parameters
The following request parameter list only provides API request parameters. Other common parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/api/213/15692).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| SAMLAssertion | Yes | String | Base64-encoded SAML assertion |
| PrincipalArn | Yes | String | Name of the resource accessible to the principal |
| RoleArn | Yes | String | Name of the resource accessible to the role |
| RoleSessionName | Yes | String | Session name |

### Output parameters
| Parameter Name | Type | Description |
|---------|---------|---------|
| credentials | [credentials](#dataStructure) | The object contains a triad of token, tmpSecretId and tmpSecretKey. |
| expiredTime | Integer |Temporary certificate expiration time (Unix timestamp in second) |
| expiration | String | Temporary certificate expiration time (UTC time in ISO8601 format) |

<span id="dataStructure"></span>
### Credential Data Structures 

| Parameter Name | Type |Description |
|---------|---------|---------|
| token | String | Token value |
| tmpSecretId | String | Temporary security certificate ID|
| tmpSecretKey | String |Temporary security certificate Key |


### Example
Create a SAML identity provider named IdP.

##### Input example:

``` 
POST /v2/index.php HTTP/1.1
Host: sts.api.qcloud.com
Accept: */*
Content-Length: 3927
Content-Type: application/x-www-form-urlencoded

Action=AssumeRoleWithSAML
&PrincipalArn=qcs::cam::uin/798950673:saml-provider/OneLogin
&RoleArn=qcs::cam::uin/798950673:roleName/OneLogin-Role
&RoleSessionName=test
&SAMLAssertion=c2FtbCBhc3NlcnRpb24=
&<Common request parameters>
``` 
##### Output example:

``` 
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "credentials": {
            "sessionToken": "d154fa74af184dfac3deb3a729c103a3003d52f840001",
            "tmpSecretId": "AKID7byWjIxUdUuRfhuctpd2T7XLpkCeqMub",
            "tmpSecretKey": "LN1yqrCt2oejxQB7AQsL8iP9VE4hzfZ9"
        },
        "expiredTime": 1541594376,
        "expiration": "2018-11-07T12:39:36Z"
    }
}
``` 

### Error codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/598/13884).

| Error Code | Description |
|---------|---------|
| InvalidParameter.ProviderNotExist | The IdP already exists. |
| InvalidParameter.SAMLResponse | Invalid SAML assertion response |
| InvalidParameter.InvalidRoleArn | Invalid name of the role allowed to access |

