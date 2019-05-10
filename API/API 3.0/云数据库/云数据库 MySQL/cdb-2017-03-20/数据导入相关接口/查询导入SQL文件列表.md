## 1. 接口描述

接口请求域名： cdb.tencentcloudapi.com 。

本接口(DescribeUploadedFiles)用于查询用户导入的SQL文件列表。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见[公共请求参数](/document/api/236/15833)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DescribeUploadedFiles |
| Version | 是 | String | 公共参数，本接口取值：2017-03-20 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| Path | 是 | String | 文件路径。该字段应填用户主账号的OwnerUin信息。 |
| Offset | 否 | Integer | 记录偏移量，默认值为0。 |
| Limit | 否 | Integer | 单次请求返回的数量，默认值为20。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| TotalCount | Integer | 符合查询条件的SQL文件总数。|
| Items | Array of [SqlFileInfo](/document/api/236/15878#SqlFileInfo) | 返回的SQL文件列表。|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 查询导入SQL文件列表

#### 输入示例

```
https://cdb.tencentcloudapi.com/?Action=DescribeUploadedFiles
&Path=100000983328
&<公共请求参数>
```

#### 输出示例

```
{
    "Response":{
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "TotalCount":1,
        "Items":[
            {
                "UploadTime":"2016-11-28 15:16:13",
                "UploadInfo":{
                    "AllSliceNum":5,
                    "CompleteNum":3
                },
                "FileName":"joellwang.sql",
                "FileSize":8581633,
                "IsUploadFinished":0,
                "FileId":"5596d7433fe211da4b487228db4e7c57",
                "Access_url": "http://xxxxxx-xxxxxxx.file.myqcloud.com:8080/100000983328/task.sql"
            }
        ]        
    }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=DescribeUploadedFiles)

### SDK

云 API 3.0 提供了配套的开发工具集（SDK），支持多种编程语言，能更方便的调用 API。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### 命令行工具

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. 错误码

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见[公共错误码](/document/api/236/15835#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| InternalError.CosError | 获取文件信息失败。 |
| InvalidParameter | 参数错误。 |
