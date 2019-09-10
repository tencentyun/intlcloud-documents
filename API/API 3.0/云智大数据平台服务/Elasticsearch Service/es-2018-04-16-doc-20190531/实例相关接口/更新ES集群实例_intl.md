## 1. API Description

API domain name: es.tencentcloudapi.com.

This API performs operations such as scaling a cluster, renaming an instance, modifying configuration, resetting password, and setting Kibana blacklist/whitelist. InstanceId is required, while ForceRestart is optional. Other parameters or parameter groups and their meaning are as follows:
- InstanceName: Rename an instance (only for instance identification)
- NodeNum: Number of nodes to be added to or removed from the cluster
- NodeType, DiskSize: Vertically scale data nodes in the cluster
- MasterNodeNum: Number of dedicated master nodes to be added to or removed from the cluster
- MasterNodeType, MasterNodeDiskSize: Vertically scale dedicated master nodes in the cluster
- EsConfig: Modify cluster configuration
- Password: Change the password of the default user elastic
- EsAcl: Modify the ACL
- CosBackUp: Configuration of auto-backup to COS for ES cluster
You can only pass in one of the above parameters or parameter groups at a time, otherwise, the request will fail.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if a financial region, such as ap-shanghai-fsi, is assigned to the common parameter Region, we recommend you include that financial region in your domain name  , such as es.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/845/30623).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: UpdateInstance |
| Version | Yes | String | Common parameter. The version of this API: 2018-04-16 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/845/30623#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID |
| InstanceName | No | String | Instance name, which can contain 1 to 50 English letters, Chinese characters, digits, dashes - or underscores _ |
| NodeNum | No | Integer | Number of nodes (2-50) |
| EsConfig | No | String | Configuration item (JSON string). Currently, only the following items are supported: <li>action.destructive_requires_name</li><li>indices.fielddata.cache.size</li><li>indices.query.bool.max_clause_count</li> |
| Password | No | String | Password of the default user elastic, which must contain 8 to 16 characters, including at least two out of the following three types of characters: [a-z,A-Z], [0-9] and [-!@#$%&^*+=_:;,.?] |
| EsAcl | No | [EsAcl](/document/api/845/30634#EsAcl) | Access control list |
| DiskSize | No | Integer | Disk size in GB |
| NodeType | No | String | Node specification <li>ES.S1.SMALL2: 1-core 2 GB </li><li>ES.S1.MEDIUM4: 2-core 4 GB </li><li>ES.S1.MEDIUM8: 2-core 8 GB </li><li>ES.S1.LARGE16: 4-core 16 GB </li><li>ES.S1.2XLARGE32: 8-core 32 GB </li><li>ES.S1.4XLARGE32: 16-core 32 GB </li><li>ES.S1.4XLARGE64: 16-core 64 GB </li> |
| MasterNodeNum | No | Integer | Number of dedicated master nodes (only 3 and 5 are supported) |
| MasterNodeType | No | String | Dedicated master node specification <li>ES.S1.SMALL2: 1-core 2 GB</li><li>ES.S1.MEDIUM4: 2-core 4 GB</li><li>ES.S1.MEDIUM8: 2-core 8 GB</li><li>ES.S1.LARGE16: 4-core 16 GB</li><li>ES.S1.2XLARGE32: 8-core 32 GB</li><li>ES.S1.4XLARGE32: 16-core 32 GB</li><li>ES.S1.4XLARGE64: 16-core 64 GB</li> |
| MasterNodeDiskSize | No | Integer | Dedicated master node disk size in GB. Default is 50 GB; customized disk size is currently not available. |
| ForceRestart | No | Boolean | Whether to force restart after configuration update <li>true: Yes </li><li>false: No </li>This needs to be set only for EsConfig. false by default |
| CosBackup | No | [CosBackup](/document/api/845/30634#CosBackup) | Configuration of auto-backup-to-COS |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Examples

### Example 1. Renaming an ES Cluster Instance

Rename the specified ES cluster instance

#### Input Sample Code

```
https://es.tencentcloudapi.com/?Action=UpdateInstance
&InstanceId=es-4texbn20
&InstanceName=newName
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "c96a110c-7493-452d-a99b-683d0711dada"
  }
}
```

### Example 2. Horizontally Scaling an ES Cluster

Horizontally scale the specified ES cluster (only horizontal scaling is supported currently)

#### Input Sample Code

```
https://es.tencentcloudapi.com/?Action=UpdateInstance
&InstanceId=es-4texbn20
&NodeNum=5
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "6001962a-17c5-4604-a0af-0d4719c2ddca"
  }
}
```

### Example 3. Modifying ES Cluster Instance Configuration

Modify the configuration of the specified ES cluster instance

#### Input Sample Code

```
https://es.tencentcloudapi.com/?Action=UpdateInstance
&InstanceId=es-4texbn20
&EsConfig={"action.destructive_requires_name":"true"}
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "e7c1bb22-e5f2-42f1-8a12-a97a6de62798"
  }
}
```

### Example 4. Resetting Kibana Password

Reset the Kibana password of the specified ES cluster instance

#### Input Sample Code

```
https://es.tencentcloudapi.com/?Action=UpdateInstance
&InstanceId=es-qlpn5o2a
&Password=newPwd_123
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "1b72089e-720f-4f95-a4ae-4da4611bdb10"
  }
}
```

### Example 5. Setting Kibana Access Blacklist/Whitelist

Set the Kibana access blacklist/whitelist for the specified ES cluster instance

#### Input Sample Code

```
https://es.tencentcloudapi.com/?Action=UpdateInstance
&InstanceId=es-qlpn5o2a
&EsAcl.BlackIpList.0=127.0.0.1
&EsAcl.BlackIpList.1=0.0.0.0
&EsAcl.WhiteIpList.0=127.0.0.1
&EsAcl.WhiteIpList.1=0.0.0.0
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "3b90bdbf-6f73-443e-958a-0b81e57ff6cb"
  }
}
```

### Example 6. Vertically Scaling an ES Cluster

Vertically scale the node specification (number of cores and memory size) and disk size in a cluster (currently, only vertical scaling is supported)

#### Input Sample Code

```
https://es.tencentcloudapi.com/?Action=UpdateInstance
&InstanceId=es-qlpn5o2a
&NodeType=ES.S1.MEDIUM4
&DiskSize=150
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "dd3f624d-9a72-4057-85cb-f5d32e7b3c7b"
  }
}
```

### Example 7. Setting Auto-backup to COS for ES

#### Input Sample Code

```
https://es.tencentcloudapi.com/?Action=UpdateInstance
&InstanceId=es-qlpn5o2a
&CosBackup.IsAutoBackup=true
&CosBackup.BackupTime=23:00
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "dd3f624d-9a72-4057-85cb-f5d32e7b3c7b"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=es&Version=2018-04-16&Action=UpdateInstance)

### SDK

TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/845/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.NoPayment | No credit card or PayPal account is bound to the current account. Unable to make a payment. |
| InternalError | Internal error. |
| InvalidParameter | Incorrect parameter. |
| ResourceInUse | Resource is occupied. |
| ResourceInsufficient | Insufficient resource. |
| ResourceInsufficient.Balance | Insufficient account balance. |
| UnsupportedOperation | Unsupported operation. |
