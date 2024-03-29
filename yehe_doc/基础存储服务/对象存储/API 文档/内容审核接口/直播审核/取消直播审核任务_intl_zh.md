## 功能描述

本接口用于取消一个在进行中的直播审核任务，成功取消后将返回已终止任务的 JobID。

## 限制说明

默认接口请求频率限制：20次/秒。

## 请求

#### 请求示例

```plaintext
POST /video/cancel_auditing/<jobId> HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>

<body>
```

>? 
> - Authorization: Auth String （详情请参见 [请求签名](https://intl.cloud.tencent.com/document/product/436/7778) 文档）。
> - 通过子账号使用时，需要授予相关的权限，详情请参见数据万象授权粒度详情 文档。
>

#### 请求头

此接口仅使用公共请求头部，详情请参见 [公共请求头部](https://intl.cloud.tencent.com/document/product/1045/43609) 文档。

#### 请求体

该请求无请求体。

## 响应

#### 响应头

此接口仅返回公共响应头部，详情请参见 [公共响应头部](https://intl.cloud.tencent.com/document/product/1045/43610) 文档。

#### 响应体

该响应体返回为 **application/xml** 数据，包含完整节点数据的内容展示如下：

```plaintext
<Response>
    <JobsDetail>
      <DataId></DataId>
      <JobId></JobId>
      <CreationTime></CreationTime>
    </JobsDetail>
    <RequestId></RequestId>
</Response>
```

具体的数据内容如下：

| 节点名称（关键字） | 父节点 | 描述                         | 类型      |
| :----------------- | :----- | :--------------------------- | :-------- |
| Response           | 无     | 直播审核返回的具体响应内容。 | Container |

Container 节点 Response 的内容：

| 节点名称（关键字） | 父节点   | 描述                                                         | 类型      |
| :----------------- | :------- | :----------------------------------------------------------- | :-------- |
| JobsDetail         | Response | 直播流审核任务的详细信息。                                   | Container |
| RequestId          | Response | 每次请求发送时，服务端将会自动为请求生成一个 ID，遇到问题时，该 ID 能更快地协助定位问题。 | String    |

Container 节点 JobsDetail 的内容：

| 节点名称（关键字） | 父节点              | 描述                       | 类型   |
| :----------------- | :------------------ | :------------------------- | :----- |
| DataId             | Response.JobsDetail | 请求中添加的唯一业务标识。 | String |
| JobId              | Response.JobsDetail | 本次直播审核任务的 ID。    | String |
| CreationTime       | Response.JobsDetail | 直播审核任务的创建时间。   | String |

#### 错误码

该请求操作无特殊错误信息，常见的错误信息请参见 [错误码](https://intl.cloud.tencent.com/document/product/1045/43611) 文档。

## 实际案例

#### 请求

```plaintext
POST /video/cancel_auditing/<jobId> HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
```

#### 响应

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
  <JobsDetail>
    <DataId>123-fdrsg-123</DataID>
    <JobId>vab1ca9fc8a3ed11ea834c525400863904</JobId>
    <CreationTime>2021-08-07T12:12:12+0800</CreationTime>
  </JobsDetail>
  <RequestId>xxxxxxxxxxxxxx</RequestId>
</Response>
```
