# 目标

本文主要介绍如何使用第三方播放器播放云点播加密视频（SimpleAES）。

# 概要

您只需要获取到视频的播放信息，然后使用第三方播放器，即可完成加密视频的解密播放。

相关播放信息如下：

- DrmToken (用于获取视频解密密钥)。
- 内容 URL。

## 架构流程图

### 私有加密

![](https://qcloudimg.tencent-cloud.cn/raw/0869fb5666a8d93a57ae0202f7468c97.jpg)

- 获取播放信息和签名
  在通过业务鉴权后，APP 服务端向 APP 终端派发播放信息以及签名（DrmToken）。

- 下载视频内容和获取密钥信息

  在获取播放信息（DrmToken、内容 URL）后，生成播放 URL，播放器触发播放，并同时触发获取密钥信息的请求。

  如果密钥受到保护，则点播密钥派发服务会对内容密钥进行加密。例如，保护模式为`sha256`，那么点播密钥派发服务会使用对称密钥对内容密钥进行加密。
  
  如果密钥没有收到保护，则点播密钥派发服务会直接派发内容密钥。

- 在获取到密钥信息后，进行解密和播放

  如果密钥受到保护，那么  APP 终端需解密才能得到内容密钥。例如，保护模式为`sha256`，那么 APP 终端需使用对称密钥对获取到的密钥信息进行解密，才能得到内容密钥，并实现视频的解密和播放。

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
  "protectSchema": "sha256",
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
| protectSchema    | string     | 否           | 保护模式，仅对 `SimpleAES` 生效。取值有 `sha256`，表示使用 `sha256(pkey)` 作为对称密钥加密内容密钥，其中`pkey`是播放密钥，`sha256`是 SHA256 哈希算法。 |

### Signatrue

#### 计算方式

`Signature = HMACSHA256(base64UrlEncode(Header) + "." + base64UrlEncode(Payload), pkey)`

?HMACSHA256 请参见 [RFC - HMACSHA256](https://tools.ietf.org/html/rfc4868#page-3)。base64UrlEncode 请参见 [RFC - base64UrlEncode](https://tools.ietf.org/html/rfc4648#page-7)。

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
  "protectSchema": "sha256",
  "issuer": "client"
}
```

base64UrlEncode 编码后为`eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsInByb3RlY3RTY2hlbWEiOiJzaGEyNTYiLCJpc3N1ZXIiOiJjbGllbnQifQ`。

- `Signature` 使用 `pkey` （假设为`JduzsUuRvGVPRHvIYwLv`）加密后为 `dK42jB0KP4sXCd7Dunng9AcQ2WlnANuB87PwxmTc3_g`。

那么，将 `Header`、`PayLoad`、`Signature` 通过`~`拼接后，`DrmToken` 则为`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsInByb3RlY3RTY2hlbWEiOiJzaGEyNTYiLCJpc3N1ZXIiOiJjbGllbnQifQ~JZ0sAV214-7vNckjb-llSntnqsIr-qF5oD4Lv7L1qGQ`。

# 如何生成播放 URL

- 通过调用 [DescribeMediaInfos](https://intl.cloud.tencent.com/document/product/266/34181) 接口可获取内容 URL。内容 URL 为返回结果中的 `MediaInfoSet.AdaptiveDynamicStreamingInfo.AdaptiveDynamicStreamingSet.Url `字段。

- 如果开启 KEY 防盗链，可参考 [KEY 防盗链](https://intl.cloud.tencent.com/document/product/266/33986) 生成带防盗链签名的内容 URL。

- 对于 `SimpleAES`，需要按照以下方式构造播放 URL：

  假设原始内容 URL 为： `http(s)://xxx.com/xxx/xxx/test.m3u8`

  那么播放 URL 为： `http(s)://xxx.com/xxx/xxx/voddrm.token.<DrmToken>.test.m3u8`

  其中文件名增加`voddrm.token.` 前缀，`<DrmToken>` 则使用上述生成的 `DrmToken`填充。
  
### 示例

假设内容 URL 为 ` https://1500014561.vod2.myqcloud.com/4395be81vodtranscq1500014561/8f8e01fb387702307091793695/adp.12.m3u8?t=9ee2bdd0&sign=46f6120466d6e931ad792bad8e4f8dff `

`DrmToken` 为`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsInByb3RlY3RTY2hlbWEiOiJzaGEyNTYiLCJpc3N1ZXIiOiJjbGllbnQifQ~JZ0sAV214-7vNckjb-llSntnqsIr-qF5oD4Lv7L1qGQ`

那么最终的播放 URL 为`https://1500014561.vod2.myqcloud.com/4395be81vodtranscq1500014561/8f8e01fb387702307091793695/voddrm.token.eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsInByb3RlY3RTY2hlbWEiOiJzaGEyNTYiLCJpc3N1ZXIiOiJjbGllbnQifQ~JZ0sAV214-7vNckjb-llSntnqsIr-qF5oD4Lv7L1qGQ.adp.12.m3u8?t=9ee2bdd0&sign=46f6120466d6e931ad792bad8e4f8dff`

# 使用第三方播放器播放

在生成到播放 URL 后，即可使用第三方播放器播放加密视频。但从点播密钥派发服务获取到密钥信息（即内容密钥密文）后，需自行实现解密逻辑。

播放器在播放加密视频时会触发获取密钥信息（即内容密钥密文，`CipherContentKey`）的请求，该请求 URL 由`m3u8`文件中的`#EXT-X-KEY`指定。如：

```text
#EXT-X-KEY:METHOD=AES-128,URI="https://drm.vod2.myqcloud.com/getlicense/v1?drmType=SimpleAES&token=<DrmToken>"
```

解密方式如下：

- 首先生成对称密钥（`SymmetricKey`）：

  `SymmetricKey=SHA256(pkey)`

  其中，`SHA256` 表示 `SHA256` 哈希算法，`pkey`表示播放密钥。

- 最后解密得到内容密钥（`ContentKey`）：

  `ContentKey=AES-CBC-Descrypt(CipherContentKey, SymmetricKey, IV)`

  其中，`CipherContentKey`为内容密钥密文，由点播密钥派发服务返回，密文中不包含初始向量 IV 的数据。`AES-CBC-Descrypt`表示采用 AES-CBC 算法进行解密，IV 为初始向量，固定为`0x00000000000000000000000000000000`。

## 解密示例

假设：

- 播放密钥（`pkey`）为`JduzsUuRvGVPRHvIYwLv`，那么对称密钥（`SymmetricKey`）为`0xece0bae38fbbd66f79c62acefb9ea994dc834d79b45cc4556962d9f00508b9b3 `(32 Bytes)。
- 内容密钥密文（`CipherContentKey`）为` 0x68addf7984478a3e4797d3a13ecbb6fb `(16 Bytes)。
- 初始向量 IV 始终为` 0x00000000000000000000000000000000`(16 Bytes)。

那么，最终内容密钥（`ContentKey`）为`0xbed3747b8510b040826163c04956a4c1`(16 Bytes)。

# 总结

至此，你已经掌握了如何使用第三方播放器播放云点播加密视频。