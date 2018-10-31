## 1. API Description

Domain name for API request: mariadb.tencentcloudapi.com

This API (CreateAccount) is used to create database accounts. Multiple accounts can be created for one instance. The same user name with a different host represents a different account.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: mariadb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/237/16147).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: CreateAccount. |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12. |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/237/16147#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID, such as tdsql-ow728lmc. It can be obtained by querying instance details via DescribeDBInstances. |
| UserName | Yes | String | Login user name, with a length of 1-32 characters comprised of letters, numbers, underscores and hyphens. |
| Host | Yes | String | CVMs available for login, which are consistent with the host format of MySQL accounts. Wildcards are supported, such as %, 10.%, and 10.20.%. |
| Password | Yes | String | The account password, with a length of 6-32 characters comprised of letters, numbers or common symbols (excluding semicolons, single quotes and double quotes). |
| ReadOnly | No | Integer | Indicates whether to create the account as a read-only one. 0: No; 1: Slave is preferred for the SQL request of the account. Master is used when slave is not available; 2: Slave is preferred. The operation fails if the slave is not available. |
| Description | No | String | Account remarks, with a length of 0-256 characters comprised of letters, common symbols and numbers. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| InstanceId | String | Instance ID. Not null. |
| UserName | String | User name. Not null. |
| Host | String | The host name part of the account or role name. Not null. |
| ReadOnly | Integer | Not null |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Create an access account for a database instance

#### Input example

```
https://mariadb.tencentcloudapi.com/?Action=CreateAccount
&InstanceId=tdsql-fdpjf5zh
&UserName=testuser1
&Host=172.17.%
&Password=1234qweri#
&Description=Test account
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "Host": "172.17.%",
    "InstanceId": "tdsql-fdpjf5zh",
    "Readonly": 0,
    "RequestId": "2cc4e4dc-c3e9-4858-ab80-03e3526cf24d",
    "UserName": "testuser1"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mariadb&Version=2017-03-12&Action=CreateAccount)

### SDK

Cloud API 3.0 comes with the software development kit (SDK) that supports multiple programming languages and makes it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### Command line tools

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to the API business logic. For other error codes, see [Common Error Codes](/document/api/237/16149#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.CreateUserFailed | Failed to create the account |
| FailedOperation.OssOperationFailed | Failed to request backend APIs |
| InternalError.CamAuthFailed | CAM authentication request failed |
| InternalError.DbOperationFailed | Failed to query the database |
| InternalError.GetUserListFailed | Failed to obtain the account list |
| InvalidParameter.CharacterError | The password contains invalid character(s) |
| InvalidParameter.GenericParameterError | Failed to pass the parameter validity verification |
| InvalidParameterValue.AccountAlreadyExists | The account already exists |
| InvalidParameterValue.SuperUserForbidden | The system user is not allowed to perform the operation |
| ResourceUnavailable.InstanceAlreadyDeleted | The database instance has been deleted |
| ResourceUnavailable.InstanceHasBeenLocked | The database instance is locked and cannot be operated |
| ResourceUnavailable.InstanceStatusAbnormal | The database instance is in an invalid status and cannot be operated |
| UnauthorizedOperation.PermissionDenied | No permission to perform operations on the API or resource |
| UnsupportedOperation.OldProxyVersion | Proxy software version is too low. Contact the customer service for upgrade and try again. |

