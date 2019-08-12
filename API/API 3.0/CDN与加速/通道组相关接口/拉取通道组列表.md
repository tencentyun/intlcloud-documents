## 1. 接口描述

接口请求域名： gaap.tencentcloudapi.com 。

本接口（DescribeProxyGroupList）用于拉取通道组列表及各通道组基本信息。

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/608/36935)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DescribeProxyGroupList |
| Version | 是 | String | 公共参数，本接口取值：2018-05-29 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| Offset | 是 | Integer | 偏移量，默认值为0。 |
| Limit | 是 | Integer | 返回数量，默认值为20，最大值为100。 |
| ProjectId | 是 | Integer | 项目ID。取值范围：<br/>-1，该用户下所有项目<br/>0，默认项目<br/>其他值，指定的项目 |
| TagSet.N | 否 | Array of [TagPair](/document/api/608/37023#TagPair) | 标签列表，当存在该字段时，拉取对应标签下的资源列表。<br/>最多支持5个标签，当存在两个或两个以上的标签时，满足其中任意一个标签时，该通道组会被拉取出来。 |
| Filters.N | 否 | Array of [Filter](/document/api/608/37023#Filter) | 过滤条件。   <br/>每次请求的Filter.Values的上限为5。<br/>RealServerRegion - String - 是否必填：否 -（过滤条件）按照源站地域过滤，可参考DescribeDestRegions接口返回结果中的RegionId。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| TotalCount | Integer | 通道组总数。|
| ProxyGroupList | Array of [ProxyGroupInfo](/document/api/608/37023#ProxyGroupInfo) | 通道组列表。<br/>注意：此字段可能返回 null，表示取不到有效值。|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 查询通道组列表

#### 输入示例

```
https://gaap.tencentcloudapi.com/?Action=DescribeProxyGroupList
&ProjectId=0
&Offset=0
&Limit=20
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "TotalCount": 2,
    "RequestId": "8b6bb93c-0dce-4513-a274-1410f276307c",
    "ProxyGroupList": [
      {
        "Status": 0,
        "Domain": null,
        "ProjectId": 0,
        "GroupName": "t4",
        "TagSet": [],
        "RealServerRegionInfo": {
          "RegionId": "EastChina",
          "RegionName": "EastChina"
        },
        "GroupId": "lg-mh4k07v5"
      },
      {
        "Status": 0,
        "Domain": null,
        "ProjectId": 0,
        "GroupName": "sandytest2",
        "TagSet": [],
        "RealServerRegionInfo": {
          "RegionId": "EastChina",
          "RegionName": "EastChina"
        },
        "GroupId": "lg-d5y6ei3b"
      }
    ]
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gaap&Version=2018-05-29&Action=DescribeProxyGroupList)

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

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见 [公共错误码](/document/api/608/36938#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| FailedOperation | 操作失败 |
| InternalError | 内部错误 |
| InvalidParameter | 参数错误 |
| InvalidParameterValue | 参数取值错误 |
| MissingParameter | 缺少参数错误 |
| ResourceNotFound | 资源不存在 |
| ResourceUnavailable | 资源不可用 |
| UnauthorizedOperation | 未授权操作 |
| UnknownParameter | 未知参数错误 |
