### API Description
This API (UpdateSAMLProvider) is used to update the description or the metadata document of an SAML IdP.
Request domain name: cam.api.qcloud.com
Request method: HTTP POST

### Input parameters
The following request parameter list only provides API request parameters. Other common parameters can be found in [Common Request Parameters](https://cloud.tencent.com/document/api/213/15692).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| name | Yes | String | SAML IdP name |
| desc | No | String | IdP description |
| SAMLMetadataDocument | No | String | SAML IdP metadata document, which must be Base64 encoded and is limited to 64 KB. |

Note: If the IdP metadata document exceeds the upper limit, the XML nodes except IDPSSODescriptor can be deleted from the XML metadata document.

### Output parameters

None.


### Example

Update the description and the metadata document of the SAML IdP named IdP.

##### Input example:

``` 
POST /v2/index.php HTTP/1.1
Host: cam.api.qcloud.com
Accept: */*
Content-Length: 3927
Content-Type: application/x-www-form-urlencoded

Action=UpdateSAMLProvider&name=idp&SAMLMetadataDocument=U0FNTE1ldGFkYXRhRG9jdW1lbnQgdjI=&desc=descriptor2&<Common request parameters>
``` 
##### Output example:

``` 
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": [
    ]
}
``` 

### Error codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/213/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidParameter.ProviderNotExist | The IdP does not exist. |
| InvalidParameter.SAMLMetadataDocument | Invalid SAML IdP metadata document |

