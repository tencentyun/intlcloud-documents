### API Description

This API (ListSAMLProviders) is used to obtain a list of SAML IdPs.
Request domain name: cam.api.qcloud.com

### Input parameters
The following request parameter list only provides API request parameters. Other common parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/api/213/15692).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| page | Yes | Integer | Page number |
| rp | Yes | Integer | Page size |

### Output parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| total | Integer | Total number of IdPs |
| list | Array Of SAMLProvider | List of SAML IdPs |

SAMLProvider contains the following fields:

| Name | Type | Description |
|---------|---------|---------|
| name | String | IdP name |
| desc | String | IdP description |
| createTime | Date | Creation time of IdP |
| modifyTime | Date | Updated time of IdP |


### Example

Query the list of SAML IdPs.

##### Input example:

``` 
https://cam.api.qcloud.com/v2/index.php?Action=ListSAMLProviders
&page=1
&rp=5
&<Common request parameters>
``` 

##### Output example:

``` 
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "total": 9,
        "list": [
            {
                "name": "api-test-v2",
                "desc": "API test 12121",
                "createTime": "2018-10-30 14:43:37",
                "modifyTime": "2018-10-30 14:57:35"
            },
            {
                "name": "api-test",
                "desc": "API test",
                "createTime": "2018-10-30 11:40:19",
                "modifyTime": "2018-10-30 11:40:19"
            },
            {
                "name": "aaaaaaaaaaa",
                "desc": "Test",
                "createTime": "2018-10-17 17:16:17",
                "modifyTime": "2018-10-17 17:16:17"
            },
            {
                "name": "test1112222",
                "desc": "111111",
                "createTime": "2018-10-15 21:30:08",
                "modifyTime": "2018-10-15 21:30:08"
            },
            {
                "name": "test111",
                "desc": "111111",
                "createTime": "2018-10-12 18:09:19",
                "modifyTime": "2018-10-12 18:09:19"
            }
        ]
    }
}
``` 

### Error codes
The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/598/13884).


