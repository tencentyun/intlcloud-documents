### API Description
This API (AssumeRoleWithSAML) is used to apply for temporary credentials for a role based on SAML assertion.
Request domain name: sts.api.qcloud.com
Request method: HTTP POST

### Input parameters
The following request parameter list only provides API request parameters. Other common parameters can be found in [Common Request Parameters](https://cloud.tencent.com/document/api/213/15692).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| SAMLAssertion | Yes | String | Base64-encoded SAML assertion |
| PrincipalArn | Yes | String | Name of the principal allowed to access |
| RoleArn | Yes | String | Name of the role allowed to access |
| RoleSessionName | Yes | String | Session name |

### Output parameters
| Parameter Name | Type | Description |
|---------|---------|---------|
| credentials | [credentials](#dataStructure) | The object contains a triad of token, tmpSecretId and tmpSecretKey. |
| expiredTime | Integer | Expiration time of the certificate, expressed in a Unix timestamp with an accuracy down to seconds. |
| expiration | String | Expiration time of certificate, expressed in a UTC time in ISO8601 format. |

<span id="dataStructure"></span>
### Data Structures of Credentials

| Parameter Name | Type |Description |
|---------|---------|---------|
| token | String | The value of token |
| tmpSecretId | String | ID of the temporary security certificate |
| tmpSecretKey | String | Key of the temporary security certificate |


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

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/213/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidParameter.ProviderNotExist | The IdP already exists. |
| InvalidParameter.SAMLResponse | Invalid SAML assertion response |
| InvalidParameter.InvalidRoleArn | Invalid name of the role allowed to access |

