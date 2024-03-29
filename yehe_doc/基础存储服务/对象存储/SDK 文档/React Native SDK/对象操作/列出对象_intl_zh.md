## 简介

本文档提供关于列出对象操作相关的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket（List Objects）](https://intl.cloud.tencent.com/document/product/436/30614) | 查询对象列表   | 查询存储桶下的部分或者全部对象     |

## 查询对象列表

#### 功能说明

查询存储桶下的部分或者全部对象。

#### 示例代码一: 获取第一页数据

```ts
// 存储桶名称，由 bucketname-appid 组成，appid 必须填入，可以在 COS 控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
let bucket = "examplebucket-1250000000";
try {
  let bucketContents: BucketContents = await Cos.getDefaultService().getBucket(
    bucket,
    {
      prefix: "dir/", // 前缀匹配，用来规定返回的对象前缀地址
      maxKeys: 100 // 单次返回最大的条目数量，默认1000
    }
  );
  // 表示数据被截断，需要拉取下一页数据
  let isTruncated = bucketContents.isTruncated;
  // nextMarker 表示下一页的起始位置
  let nextMarker = bucketContents.nextMarker;
} catch (e) {
  // 失败后会抛异常 根据异常进行业务处理
  console.log(e);
}
```

#### 示例代码二：请求下一页数据

```ts
// 存储桶名称，由 bucketname-appid 组成，appid 必须填入，可以在 COS 控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
let bucket = "examplebucket-1250000000";
// prevPageBucketContents 是上一页的返回结果，这里的 nextMarker 表示下一页的起始位置
let prevPageMarker = prevPageBucketContents.nextMarker;
try {
  let bucketContents: BucketContents = await Cos.getDefaultService().getBucket(
    bucket,
    {
      prefix: "dir/", // 前缀匹配，用来规定返回的对象前缀地址
      marker: prevPageMarker, // 起始位置
      maxKeys: 100 // 单次返回最大的条目数量，默认1000
    }
  );
  // 表示数据被截断，需要拉取下一页数据
  let isTruncated = bucketContents.isTruncated;
  // nextMarker 表示下一页的起始位置
  let nextMarker = bucketContents.nextMarker;
} catch (e) {
  // 失败后会抛异常 根据异常进行业务处理
  console.log(e);
}
```

#### 示例代码三：获取对象列表与子目录

```ts
// 存储桶名称，由 bucketname-appid 组成，appid 必须填入，可以在 COS 控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
let bucket = "examplebucket-1250000000";
// 定界符为一个符号，如果有 Prefix，
// 则将 Prefix 到 delimiter 之间的相同路径归为一类，定义为 Common Prefix，
// 然后列出所有 Common Prefix。如果没有 Prefix，则从路径起点开始
let delimiter = "/";
try {
  let bucketContents: BucketContents = await Cos.getDefaultService().getBucket(
    bucket,
    {
      prefix: "dir/", // 前缀匹配，用来规定返回的对象前缀地址
      delimiter: delimiter,
      maxKeys: 100 // 单次返回最大的条目数量，默认1000
    }
  );
  // 表示数据被截断，需要拉取下一页数据
  let isTruncated = bucketContents.isTruncated;
  // nextMarker 表示下一页的起始位置
  let nextMarker = bucketContents.nextMarker;
} catch (e) {
  // 失败后会抛异常 根据异常进行业务处理
  console.log(e);
}
```

#### 参数说明

| 参数名称   | 描述                                                         | 类型   | 是否必选 |
| ---------- | ------------------------------------------------------------ | ------ | ------ |
| bucket | 桶名称，Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String | 是 |
| prefix | 对象键匹配前缀，限定响应中只包含指定前缀的对象键 | String | 否 |
| delimiter | 一个字符的分隔符，用于对对象键进行分组。所有对象键中从 prefix 或从头（如未指定 prefix）到首个 delimiter 之间相同的部分将作为 CommonPrefixes 下的一个 Prefix 节点。被分组的对象键不再出现在后续对象列表中，具体场景和用法可参考上面的实际案例 | String | 否 |
| encodingType | 规定返回值的编码方式，可选值：url，代表返回的对象键为 URL 编码（百分号编码）后的值，例如“腾讯云”将被编码为 `%E8%85%BE%E8%AE%AF%E4%BA%91` | String | 否 |
| marker | 起始对象键标记，从该标记之后（不含）按照 UTF-8 字典序返回对象键条目 | String | 否 |
| maxKeys | 单次返回最大的条目数量，默认值为1000，最大为1000 注意：该参数会限制每一次 List 操作返回的最大条目数，COS 在每次 List 操作中将返回不超过 max-keys 所设定数值的条目（即 CommonPrefixes 和 Contents 的总和），如果单次响应中未列出所有对象，COS 会返回 NextMarker 节点，其值作为您下次 List 请求的 marker 参数，以便您列出后续对象 | Int | 否 |

#### 返回结果说明

- 成功：返回 BucketContents 包含：对象列表和列表信息。
- 失败：发生错误（如身份认证失败），抛出异常 CosXmlClientError 或者 CosXmlServiceError。详情请参见 [异常处理](https://www.tencentcloud.com/document/product/436/53970)。

BucketContents 响应包体具体数据内容如下：

| 参数名称   | 描述                                                         | 类型   |
| ---------- | ------------------------------------------------------------ | ------ |
| name | 存储桶的名称，格式为&lt;BucketName-APPID&gt;，例如 examplebucket-1250000000 | String |
| encodingType | 编码格式，对应请求中的 encodingType 参数，且仅当请求中指定了 encodingType 参数才会返回该节点 | String |
| prefix | 对象键匹配前缀，对应请求中的 prefix 参数 | String |
| marker | 起始对象键标记，从该标记之后（不含）按照 UTF-8 字典序返回对象键条目，对应请求中的 marker 参数 | String |
| maxKeys | 单次响应返回结果的最大条目数量，对应请求中的 maxKeys 参数 | Int |
| delimiter | 分隔符，对应请求中的 delimiter 参数，且仅当请求中指定了 delimiter 参数才会返回该节点 | String |
| isTruncated | 响应条目是否被截断，布尔值，例如 true 或 false | Bool |
| nextMarker | 仅当响应条目有截断（IsTruncated 为 true）才会返回该节点，该节点的值为当前响应条目中的最后一个对象键，当需要继续请求后续条目时，将该节点的值作为下一次请求的 marker 参数传入 | String |
| contentsList | 对象条目 | List&lt;Content&gt; |
| commonPrefixesList | 从 prefix 或从头（如未指定 prefix）到首个 delimiter 之间相同的部分，定义为 Common Prefix。仅当请求中指定了 delimiter 参数才有可能返回该节点 | List&lt;CommonPrefixes&gt; |

对象（Content）中包含如下内容：

| 参数名称   | 描述                                                         | 类型   |
| ---------- | ------------------------------------------------------------ | ------ |
| key | 对象键 | String |
| lastModified | 对象最后修改时间，为 ISO8601 格式，例如2019-05-24T10:56:40Z | String |
| eTag | 对象的实体标签（Entity Tag），是对象被创建时标识对象内容的信息标签，可用于检查对象的内容是否发生变化，例如 `“8e0b617ca298a564c3331da28dcb50df”`，此头部并不一定返回对象的 MD5 值，而是根据对象上传和加密方式而有所不同 | String |
| size | 对象大小，单位为 Byte | Int |
| owner | 对象持有者信息 | Owner |
| storageClass | 对象存储类型。枚举值请参见 存储类型 文档，例如 STANDARD_IA，ARCHIVE | String |

持有者信息（Owner） 中包含如下内容：

| 参数名称   | 描述                                                         | 类型   |
| ---------- | ------------------------------------------------------------ | ------ |
| id | 对象持有者的 APPID	 | String |
| disPlayName | 对象持有者的名称	 | String |

CommonPrefixes 中包含如下内容：

| 参数名称   | 描述                                                         | 类型   |
| ---------- | ------------------------------------------------------------ | ------ |
| prefix | 单条 Common Prefix 的前缀 | String |
