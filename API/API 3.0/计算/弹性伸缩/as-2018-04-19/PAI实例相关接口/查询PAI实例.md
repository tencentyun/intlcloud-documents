## 1. 接口描述

接口请求域名： as.tencentcloudapi.com 。

本接口（DescribePaiInstances）用于查询PAI实例信息。

* 可以根据实例ID、实例域名等信息来查询PAI实例的详细信息。过滤信息详细请见过滤器`Filter`。
* 如果参数为空，返回当前用户一定数量（`Limit`所指定的数量，默认为20）的PAI实例。

默认接口请求频率限制：20次/秒。

注意：本接口支持金融区地域。由于金融区和非金融区是隔离不互通的，因此当公共参数 Region 为金融区地域（例如 ap-shanghai-fsi）时，需要同时指定带金融区地域的域名，最好和 Region 的地域保持一致，例如：as.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/377/20426)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DescribePaiInstances |
| Version | 是 | String | 公共参数，本接口取值：2018-04-19 |
| Region | 是 | String | 公共参数，详见产品支持的 [地域列表](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)。 |
| InstanceIds.N | 否 | Array of String | 依据PAI实例的实例ID进行查询。 |
| Filters.N | 否 | Array of [Filter](/document/api/377/20453#Filter) | 过滤条件。 |
| Limit | 否 | Integer | 返回数量，默认为20，最大值为100。 |
| Offset | 否 | Integer | 偏移量，默认为0。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| TotalCount | Integer | 符合条件的PAI实例数量|
| PaiInstanceSet | Array of [PaiInstance](/document/api/377/20453#PaiInstance) | PAI实例详细信息|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 查询PAI实例

通过PAI实例ID查询

#### 输入示例

```
https://as.tencentcloudapi.com/?Action=DescribePaiInstances
&InstanceIds.0=ins-6he2sztp
&InnstanceIds.1=ins-0xdrree5
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "TotalCount": 2,
    "PaiInstanceSet": [
      {
        "InstanceId": "ins-6he2sztp",
        "BindingIp": "49.51.8.175",
        "DomainNameStatus": "ENABLED",
        "DomainName": "plumcot-j99466wb.pai.tcloudbase.com"
      },
      {
        "InstanceId": "ins-0xdrree5",
        "BindingIp": "45.113.71.202",
        "DomainNameStatus": "ENABLED",
        "DomainName": "berry-kotucbu9.pai.tcloudbase.com"
      }
    ],
    "RequestId": "61a4c56f-c216-42f0-8238-eeabe338633e"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribePaiInstances)

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

该接口暂无业务逻辑相关的错误码，其他错误码详见 [公共错误码](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。
