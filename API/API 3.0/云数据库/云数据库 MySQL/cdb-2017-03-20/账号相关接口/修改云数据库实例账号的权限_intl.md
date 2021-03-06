## 1. API Description

Domain name for API request: cdb.tencentcloudapi.com.

This API (ModifyAccountPrivileges) is used to modify the permissions of a database account.

A maximum of 20 requests can be initiated per second for this API.

Note: This API supports Finance regions. Since Finance regions and non-Finance regions are isolated and not interconnected. If the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region that should be identical to the value of Region field, for example: cdb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/236/15692).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: ModifyAccountPrivileges |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-20 |
| Region | Yes |  String | Common parameter. For more information, please see the [list of regions](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/236/15692#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID, such as cdb-c1nl9rpv. It is identical to the instance ID displayed in the database console page. |
| Accounts.N | Yes | Array of [Account](https://cloud.tencent.com/document/api/236/##Account) | Database account, including user name and domain name. |
| GlobalPrivileges.N | No | Array of String | Global permissions. Available values for GlobalPrivileges: "SELECT", "INSERT", "UPDATE", "DELETE", "CREATE", "DROP", "REFERENCES", "INDEX", "ALTER", "SHOW DATABASES", "CREATE TEMPORARY TABLES", "LOCK TABLES", "EXECUTE", "CREATE VIEW", "SHOW VIEW", "CREATE ROUTINE", "ALTER ROUTINE", "EVENT", and "TRIGGER". |
| DatabasePrivileges.N | No | Array of [DatabasePrivilege](https://cloud.tencent.com/document/api/236/##DatabasePrivilege) | Database permissions. Available values for Privileges: "SELECT", "INSERT", "UPDATE", "DELETE", "CREATE", "DROP", "REFERENCES", "INDEX", "ALTER", "CREATE TEMPORARY TABLES", "LOCK TABLES","EXECUTE", "CREATE VIEW", "SHOW VIEW", "CREATE ROUTINE", "ALTER ROUTINE", "EVENT", and "TRIGGER". |
| TablePrivileges.N | No | Array of [TablePrivilege](https://cloud.tencent.com/document/api/236/##TablePrivilege) | Permissions for tables in the database. Available values for Privileges: "SELECT", "INSERT", "UPDATE", "DELETE", "CREATE", "DROP", "REFERENCES", "INDEX", "ALTER", "CREATE VIEW", "SHOW VIEW", and "TRIGGER". |
| ColumnPrivileges.N | No | Array of [ColumnPrivilege](https://cloud.tencent.com/document/api/236/##ColumnPrivilege) | Permissions for columns in the database. Available values for Privileges: "SELECT", "INSERT", "UPDATE", and "REFERENCES". |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| AsyncRequestId | String | ID of async task request, which can be used to query the execution result of the async task. |
| RequestId | String | The unique request ID, which is returned for each request. RequestId is required for locating a problem. |

## 4. Error Codes

The following only lists the error codes related to the API business logic. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/236/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidParameter | Parameter error. |
| InvalidParameter.InstanceNotFound | The instance does not exist. |

## 5. Example

### Example 1 Modify the permissions of a database instance account

#### Input example

```
https://cdb.tencentcloudapi.com/?Action=ModifyAccountPrivileges
&InstanceId=cdb-f35wr6wj
&Accounts.0.user=ajnnw
&GlobalPrivileges.0=SELECT
&Accounts.0.host=127.0.0.1
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "AsyncRequestId": "256117ed-efa08b54-61784d44-91781bbd",
    "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7"
  }
}
```


## 6. Other Resources

Cloud API 3.0 comes with the following development tools to make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)
* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

