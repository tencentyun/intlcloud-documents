### API Description

This API (DeleteSAMLProvider) is used to delete a SAML IdP.
Request domain name: cam.api.qcloud.com

### Input parameters

The following request parameter list only provides API request parameters. Other common parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/api/213/15692).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| name | Yes | String | SAML IdP name |

### Output parameters

None.


### Example

Delete a SAML identity provider named IdP

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

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/598/13884).

| Error Code | Description |
|---------|---------|
| InvalidParameter.ProviderNotExist | The IdP does not exist. |

