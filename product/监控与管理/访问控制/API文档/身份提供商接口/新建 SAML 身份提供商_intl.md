### API Description

This API (CreateSAMLProvider) is used to create a SAML IdP.

Request domain name: cam.api.qcloud.com

Request method: HTTP POST

### Input parameters

The following request parameter list only provides API request parameters. Other common parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/api/213/15692).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| name | Yes | String | SAML IdP name |
| desc | Yes | String | IdP description |
| SAMLMetadataDocument | Yes | String | SAML IdP metadata document must be Base64 encoded, and its maximum size is 64 KB |

Note: If the IdP metadata document exceeds the file size limit, you can delete any of XML nodes except IDPSSODescriptor from the XML metadata document. For example:

``` 
<?xml version="1.0" encoding="utf-8"?>
<EntityDescriptor>
	<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
		......
	</IDPSSODescriptor>
</EntityDescriptor>
``` 

### Output parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| name | String | SAML IdP name |
| SAMLProviderArn | String | Name of SAML IdP |

### Example

Create a SAML identity provider named IdP.

##### Input example:

``` 
POST /v2/index.php HTTP/1.1
Host: cam.api.qcloud.com
Accept: */*
Content-Length: 3927
Content-Type: application/x-www-form-urlencoded

Action=CreateSAMLProvider&name=idp&SAMLMetadataDocument=U0FNTE1ldGFkYXRhRG9jdW1lbnQ&desc=descriptor&<Common request parameters>
``` 
##### Output example:

``` 
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "name": "idp",
        "SAMLProviderArn": "qcs::cam::uin/798950673:saml-provider/idp"
    }
}

``` 

### Error codes
The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/598/13884).

| Error Code | Description |
|---------|---------|
| InvalidParameter.ProviderAlreadyExist | The IdP already exists. |
| InvalidParameter. SAMLMetadataDocument | Invalid SAML IdP metadata document |
| InvalidParameter.ProviderMaxLimit | The number of IdPs reached the upper limit. |

