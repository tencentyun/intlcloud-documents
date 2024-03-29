## 描述

此篇文档将为您介绍在使用 API 时会出现的公共响应头部（Response Header），下文提到的头部在后续的具体 API 文档中不再赘述。

## 响应头部列表

<table>
   <tr>
      <th >Header 名称</th>
      <th>描述</th>
      <th>类型</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Content-Length</td>
      <td>RFC 2616 中定义的 HTTP 响应内容长度（字节）。</td>
      <td>string</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Content-Type</td>
      <td>RFC 2616 中定义的 HTTP 响应内容类型（MIME）。</td>
      <td>string</td>
   </tr>
   <tr>
      <td>Connection</td>
      <td>RFC 2616 中定义，表明响应完成后是否会关闭网络连接。枚举值：keep-alive，close。</td>
      <td>enum</td>
   </tr>
   <tr>
      <td>Date</td>
      <td>RFC 1123 中定义的 GMT 格式服务端响应时间，例如<code>Wed, 29 May 2019 04:10:12 GMT</code>。</td>
      <td>string</td>
   </tr>
   <tr>
      <td>ETag</td>
      <td>ETag 全称为 Entity Tag，是对象被创建时标识对象内容的信息标签，可用于检查对象的内容是否发生变化，例如<code>"8e0b617ca298a564c3331da28dcb50df"</code>。此头部并不一定返回对象的 MD5 值，而是根据对象上传和加密方式而有所不同。如果您需要校验上传到云端的文件和本地文件的一致性，我们推荐您使用 x-cos-hash-crc64ecma 头部中的 CRC64编码进行校验。</td>
      <td>string</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Last-Modified</td>
      <td>对象的最近一次上传的时间，例如<code>Fri, 10 Apr 2020 18:17:25 GMT</code>。</td>
      <td>string</td>
   </tr>
   <tr>
      <td>Server</td>
      <td>接收请求并返回响应的服务器的名称，默认值：<code>tencent-cos</code>。</td>
      <td>string</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Transfer-Encoding</td>
      <td>RFC 2616 中定义的传输编码格式。</td>
      <td>string</td>
   </tr>
   <tr>
      <td nowrap="nowrap">x-cos-hash-crc64ecma</td>
      <td>对象的 CRC64 值，详情请参见 <a href="https://intl.cloud.tencent.com/document/product/436/34078">CRC64 校验</a> 文档。</td>
      <td>integer</td>
   </tr>
   <tr>
      <td nowrap="nowrap">x-cos-request-id</td>
      <td>每次请求发送时，服务端将会自动为请求生成一个 ID。</td>
      <td>string</td>
   </tr>
   <tr>
      <td nowrap="nowrap">x-cos-trace-id</td>
      <td>每次请求出错时，服务端将会自动为这个错误生成一个 ID。仅当请求出错时才会在响应中包含此头部。</td>
      <td>string</td>
   </tr>
</table>


## 服务端加密专用头部

对于支持服务端加密（Server Side Encryption，SSE）且在请求中使用了服务端加密的接口，将根据具体的加密类型返回以下响应头，详情请参见 [服务端加密概述](https://intl.cloud.tencent.com/document/product/436/18145)。

### SSE-COS

<table>
   <tr>
      <th>Header 名称</th>
      <th>描述</th>
      <th>类型</th>
   </tr>
   <tr>
      <td nowrap="nowrap">x-cos-server-side-encryption</td>
      <td>当上传对象时使用了 SSE-COS，或者下载经过 SSE-COS 加密的对象时，请求的响应均会返回此头部，用于表明对象上传时使用的服务端加密算法。</td>
      <td>string</td>
   </tr>
</table>

### SSE-KMS

| Header 名称                                 | 描述                                                         | 类型   |
| ------------------------------------------- | ------------------------------------------------------------ | ------ |
| x-cos-server-side-encryption                | 当上传对象时使用了 SSE-KMS，或者下载经过 SSE-KMS 加密的对象时，请求的响应均会返回此头部，用于表明对象上传时使用的服务端加密算法。 | string |
| x-cos-server-side-encryption-cos-kms-key-id | 返回 KMS（密钥管理系统）的用户主密钥 CMK。如未指定，则返回 COS 默认创建的 CMK。        | string |

### SSE-C

| Header 名称        | 描述                                     | 类型   |
| ------------------ | ---------------------------------------- | ------ |
| x-cos-server-side-encryption-customer-algorithm | 当上传对象时使用了 SSE-C，或者下载经过 SSE-C 加密的对象时，请求的响应均会返回此头部，用于表明对象上传时使用的服务端加密算法。 | string |
| x-cos-server-side-encryption-customer-key-MD5 | 对象上传时使用的服务端加密密钥的 MD5 哈希值，使用 Base64 编码，<br>例如`U5L61r7jcwdNvT7frmUG8g==`。 | string |
