# 目标

本文主要介绍如何使用第三方播放器播放云点播加密视频（Widevine、FairPlay）。

# 概要

您只需要获取到视频的播放信息，然后使用第三方播放器，即可完成加密视频的解密播放。

播放信息如下：

- Widevine
  - DrmToken  (用于获取播放许可证)
  - 内容 URL
  - 播放许可证 URL （License URL）
- FairPlay
  - DrmToken   (用于获取播放许可证)
  - 内容 URL
  - 播放许可证 URL （License URL）
  - 证书 URL （Certificate URL）

## 架构流程图

### 商业级 DRM （Widevine、FairPlay）

![](https://qcloudimg.tencent-cloud.cn/raw/c77d070232e66d1eef6a6a91b5e8561e.jpg)

- 获取播放信息和签名
  APP 终端在通过业务鉴权后，APP 服务端会向 APP 终端派发播放信息以及签名（DrmToken）。

- 下载视频内容、证书，并获取 License

  在获取播放信息后，播放器触发播放，并同时触发获取许可证（ License）以及获取证书 的请求。

- 解密和播放

  在获取到 License 后，播放器使用 License 解密并播放视频。

# 如何生成 DrmToken

DrmToken 本质上是一个 [Json Web Token](https://jwt.io/introduction) (JWT) 的变形。DrmToken 也分为 Header、PayLoad、Signature 三部分，但不同的是，云点播使用~拼接这三部分。具体如下：

### Header

Header 为 JSON 格式，表示 JWT 使用的算法信息，固定使用如下内容：

```json
{
 "alg": "HS256",
 "typ": "JWT"
}
```

### PayLoad

Payload 为 JSON 格式，是播放器签名参数的内容。例如：

```json
{
  "type": "DrmToken",
  "appId": 1500014561,
  "fileId": "387702307091793695",
  "currentTimeStamp": 1650964374,
  "expireTimeStamp": 2147483647,
  "random": 4220003655,
  "issuer": "client"
}
```

#### PayLoad 参数说明

| **参数名**       | **类型**   | **是否必填** | **描述**                                                     |
| ---------------- | ---------- | ------------ | ------------------------------------------------------------ |
| type             | string     | 是           | token 类型。填写 `DrmToken`。                               |
| appId            | int64      | 是           | AppId。                                                      |
| fileId           | string     | 是           | 文件Id。                                                     |
| issuer       | string | 是       | 签发者。固定填写为 `client`。                                |
| currentTimeStamp | int64      | 是           | 当前 Unix 时间戳。                                           |
| expireTimeStamp  | int64      | 否           | 过期 Unix 时间戳。不填代表不过期。      |
| random           | int64      | 否           | 随机数。                                                     |


### Signatrue

#### 计算方式

`Signature = HMACSHA256(base64UrlEncode(Header) + "." + base64UrlEncode(Payload), pkey)`

>? HMACSHA256 请参见 [RFC - HMACSHA256](https://tools.ietf.org/html/rfc4868#page-3)。base64UrlEncode 请参见 [RFC - base64UrlEncode](https://tools.ietf.org/html/rfc4648#page-7)。

其中，播放密钥（pkey）可在控制台中查询获取。

点击点播控制台左侧导航栏**分发播放设置**>**默认分发配置**，即可在页面右侧查询到播放密钥。

![](https://qcloudimg.tencent-cloud.cn/raw/d3bebcb860f8c9900fca9a645a0879be.png)

### DrmToken 生成示例

- `Header` 内容为：

```json
{
 "alg": "HS256",
 "typ": "JWT"
}
```

base64UrlEncode 编码后为 `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`。

- `PayLoad` 为：

```json
{
  "type": "DrmToken",
  "appId": 1500014561,
  "fileId": "387702307091793695",
  "currentTimeStamp": 1650964374,
  "expireTimeStamp": 2147483647,
  "random": 4220003655,
  "issuer": "client"
}
```

base64UrlEncode 编码后为`eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsImlzc3VlciI6ImNsaWVudCJ9`。

- `Signature` 使用 `pkey` （假设为`JduzsUuRvGVPRHvIYwLv`）加密后为 `muHWnxX9dXsUAkCzw4uXGcvwKDoA19BkR-hCJVrXyvY`。

那么，将 `Header`、`PayLoad`、`Signature` 通过`~`拼接后，`DrmToken` 则为`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsImlzc3VlciI6ImNsaWVudCJ9~NN_EBW7VxGK69v-w9Q7Dw-sm8Uryfe_NdRUe3RZZ4wY`。

# 如何生成播放 URL

- 通过调用 [DescribeMediaInfos](https://intl.cloud.tencent.com/document/product/266/34181) 接口可获取内容 URL。内容 URL 为返回结果中的 `MediaInfoSet.AdaptiveDynamicStreamingInfo.AdaptiveDynamicStreamingSet.Url `字段。

- 如果开启 KEY 防盗链，可参考 [KEY 防盗链](https://intl.cloud.tencent.com/document/product/266/33986) 生成带防盗链签名的内容 URL。


# 如何生成许可证 URL

对于商业级 DRM，播放器需获取许可证（LIcense）才能解密播放视频。下面介绍如何通过许可证 URL 发起许可证请求。

## 请求

请求 URI:

- Widevine:  `https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2`
- FairPlay: `https://fairplay.drm.vod-qcloud.com/fairplay/getlicense/v2`

请求方式：`POST`

请求参数：

| **参数名**        | **描述**                                                     |
| ---------------- | ------------------------------------------------------------ |
| drmToken     | 校验凭证。 |

>? 在请求 BODY 中，则需要带上由 DRM 客户端模块生成的许可证请求数据（License Request Data）。

## 应答

- 成功，`Status Code` 为 200，并返回 License 的二进制数据。

- 失败，`Status Code` 为非 200。

### Status Code 列表
| **Status Code**        | **描述**                                                     |
| ---------------- | ------------------------------------------------------------ |
| 200     | 请求成功。 |
| 400     | 参数错误。 |
| 403     | 鉴权失败。 |
| 500     | 内部错误。 |

## 示例

根据上述请求规则，`Widevine`方案的许可证 URL 为  `https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2?drmToken=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsImlzc3VlciI6ImNsaWVudCJ9~NN_EBW7VxGK69v-w9Q7Dw-sm8Uryfe_NdRUe3RZZ4wY`

# 如何获取证书 URL

如果您需要播放使用`FairPlay`方案的加密视频，需先[申请](https://www.tencentcloud.com/document/product/266/46643)和[提交](https://www.tencentcloud.com/document/product/266/49668)`FairPlay`证书信息。对于`Widevine`方案，不需要获取证书 URL。

提交后证书信息后，可以控制台中查看证书 URL。每个子应用共用同一个证书 URL。

# 使用第三方播放器播放

在获取到播放 URL、许可证 URL、证书 URL 后，即可使用第三方播放器播放 DRM 加密视频。

# 总结

至此，你已经掌握了如何使用第三方播放器播放云点播 DRM 加密视频。