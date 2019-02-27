### API Description

This API (DeleteSAMLProvider) is used to delete an SAML IdP.
Request domain name: cam.api.qcloud.com

### Input parameters

The following request parameter list only provides API request parameters. Other common parameters can be found in [Common Request Parameters](https://cloud.tencent.com/document/api/213/15692).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| name | Yes | String | SAML IdP name |

### Output parameters

None.


### Example

Delete an SAML identity provider named IdP

##### Input example:

``` 
https://cam.api.qcloud.com/v2/index.php?Action=DeleteSAMLProvider
&name=idp
&<Common request parameters>
``` 

##### Output example:

``` 
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": []
}
``` 

### Error codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/213/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidParameter.ProviderNotExist | The IdP does not exist. |

