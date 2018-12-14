## 1. API Description
This API (CertGetList) is used to get the list of certificates.
Domain name for API request: wss.api.qcloud.com

## 2. Input Parameters
The following request parameter list only provides the API request parameters. Common request parameters are required when the API is called. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/377/4153). The Action field for this API is CertGetList.  

| Parameter Name | Required | Type | Default | Description |
|---------|---------|---------|---------|---------|
| page | No | Int | 1 | Number of pages |
| count | No | Int | 20 | Number of entries per page |
| searchKey | No | String | | Key word for search |
| certType | No | String | | Certificate type. CA: client certificate. SVR: server certificate. |
| id | No | String | | Certificate ID |
| withCert | No | Int | 0 | Indicates whether to get certificate content at the same time |
| altDomain | No | String | | Only returns to the certificates used by the domain name if passed in |
## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code. 0: Successful; other values: Failed. |
| message | String | Module error message description depending on API |
| codeDesc | String | Error code. For a successful operation, "Success" is returned. For a failed operation, a message describing the failure is returned. |
| data | Array | Data returned by the API |

If the list is obtained, the "data" field is returned, including the value of "totalNum" and "list", where
the "list" field is the basic information returned after the list is obtained:

| Parameter Name | Type | Description |
|---------|---------|---------|
| ownerUin | String | Account |
| projectId | String | Project ID |
| from | String | The source of the certificate. "trustasia" means Trust Asia, "upload" means uploaded by users |
| type | Int | Certificate type |
| certType | String | Same as the input parameter "certType" with available values of CA and SVR |
| productZhName | String | Name of the certificate authority |
| domain | String | Primary domain name |
| alias | String | Alias |
| status | Int | Status value, see "Certificate Status Information" |
| vulnerability_status | String | Vulnerability scanning status: INACTIVE = Not activated; ACTIVE = activated |
| statusMsg | String | Status information |
| verifyType | String | Verification type |
| certBeginTime | String | Time when the certificate takes effect |
| certEndTime | String | Time when the certificate expires |
| validityPeriod | String | Time when the certificate expires |
| insertTime | String | Creation time |
| projectInfo | String | Project information, see "Fields of detailed project information" |
| id | String | Certificate ID |
| subjectAltName | Array | Domain names contained by the certificate (including primary domain name) |
| type_name | String | Name of certificate type |
| status_name | String | Status name |
| is_vip | Bool | Indicates whether this is a VIP |
| is_dv | Bool | Indicates whether it is a DV certificate |
| is_wildcard | Bool | Indicates whether it is a wildcard-domain certificate |
| is_vulnerability | Bool | Indicates whether vulnerability scanning is enabled |

Certificate status:

| Parameter Value | Description |
|---------|---------|
| 0 | Verifying |
| 1 | Approved |
| 2 | Verification failed |
| 3 | Expired |
| 4 | Tencent Cloud DNS record has been added |
| 5 | OV/EV certificate to be submitted |
| 6 | Canceling orders |
| 7 | Canceled |
| 8 | Materials submitted and confirmation letter to be uploaded |


Fields of detailed project information:

| Parameter Name | Type | Description |
|---------|---------|---------|
| projectId | String | Project ID |
| ownerUin | String | uin that the project belongs to. It is 0 by default. |
| name | String | Project name |
| creatorUin | String | Creator uin |
| createTime | String | Creation time of the project |
| info | String | Project description |

## 4. Example
```
https://wss.test.api.qcloud.com/v2/index.php?
&<Common request parameters>
&Action=CertGetList
&id=xxxxxxxx
```
The returned results are as below:

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "totalNum": 12,
        "list": [
            {
                "ownerUin": "664372747",
                "projectId": "0",
                "from": "trustasia",
                "type": "2",
                "certType": "SVR",
                "productZhName": "TrustAsia TLS RSA CA",
                "domain": "cl.f-xj.cn",
                "alias": "",
                "status": 1,
                "vulnerability_status": "INACTIVE",
                "statusMsg": null,
                "verifyType": "DNS_AUTO",
                "certBeginTime": "2017-12-20 08:00:00",
                "certEndTime": "2018-12-20 20:00:00",
                "validityPeriod": "12",
                "insertTime": "2017-12-20 21:25:00",
                "projectInfo": {
                    "projectId": "0",
                    "ownerUin": 0,
                    "name": "Default Project",
                    "creatorUin": 0,
                    "createTime": "0000-00-00 00:00:00",
                    "info": "Default Project"
                },
                "id": "GjTNRoK7",
                "subjectAltName": [
                    "cl.f-xj.cn"
                ],
                "type_name": "TrustAsia TLS RSA CA",
                "status_name": "Approved",
                "is_vip": false,
                "is_dv": true,
                "is_wildcard": false,
                "is_vulnerability": false
            }
          ]
    }
}  

```

