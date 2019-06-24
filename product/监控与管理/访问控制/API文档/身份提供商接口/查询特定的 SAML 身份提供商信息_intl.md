### API Description
This API (GetSAMLProvider) is used to query the details of a specific SAML IdP.

Request domain name: cam.api.qcloud.com

### Input parameters
The following request parameter list only provides API request parameters. Other common parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/api/213/15692).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| name | Yes | String | SAML IdP name |

### Output parameters
| Parameter Name | Type | Description |
|---------|---------|---------|
| ownerUin | Integer | Tencent Cloud account ID |
| name | String | IdP name |
| desc | String | IdP description |
| createTime | Date | Creation time of IdP |
| modifyTime | Date | Last modified time of the IdP |
| SAMLMetadata | String | SAML IdP metadata document |

### Example

Query the details of the SAML identity provider named IdP.

##### Input example:

``` 
https://cam.api.qcloud.com/v2/index.php?Action=GetSAMLProvider
&name=idp
&<Common request parameters>
``` 
##### Output example:

``` 
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "ownerUin": 798950673,
        "name": "idp",
        "desc": "SAML IdP",
        "createTime": "2018-10-30 14:43:37",
        "modifyTime": "2018-10-30 14:50:39",
        "SAMLMetadata": "U0FNTE1ldGFkYXRh"
    }
}
``` 

### Error codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/598/13884).



