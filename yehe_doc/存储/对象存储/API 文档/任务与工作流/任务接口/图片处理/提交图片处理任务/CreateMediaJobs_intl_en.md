## Feature Description

This API (`CreateMediaJobs`) is used to submit an image processing job.

## Request

#### Sample request

```shell
POST /pic_jobs HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>?
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted.
>

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body
This request requires the following request body:

```shell
<Request>
  <Tag>PicProcess</Tag>
  <Input>
    <Object></Object>
  </Input>
  <Operation>
    <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
    <Output>
      <Region></Region>
      <Bucket></Bucket>
      <Object></Object>
    </Output>
  </Operation>
  <QueueId></QueueId>
  <CallBack></CallBack>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | ---- |
| Request            | None     | Request container | Container | Yes   |

<span id="Request"></span>
`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Tag                | Request | Job type: PicProcess                                   | String    | Yes   |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule                                  | Container | Yes   |
| QueueId            | Request | Queue ID of the image processing job                                         | String    | Yes   |
| CallBack           | Request | Callback address                                                | String    | No   |

<span id="Input"></span>
`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | --------------- | ------ | ---- |
| Object             | Request.Input | Media filename | String | Yes   |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | ---- |
| PicProcess         | Request.Operation | Job type parameter. Same as `Request.PicProcess` in the image processing template creation API `CreateMediaTemplate`.    | Container | No   |
| TemplateId                   | Request.Operation | Template ID                                        | String    | No  |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |

>! `TemplateId` is used first. If `TemplateId` is unavailable, the corresponding job type parameter is used.
>

<span id="Output"></span>
`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------ | ------------------------------------------------------------ | ------ | ---- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Result filename.                                             | String | Yes   |


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
  <JobsDetail>
    <Code></Code>
    <Message></Message>
    <JobId></JobId>
    <State></State>
    <CreationTime></CreationTime>
    <EndTime></EndTime>
    <QueueId></QueueId>
    <Tag>PicProcess</Tag>
    <Input>
      <Object></Object>
    </Input>
    <Operation>
      <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
      <Output>
        <Region></Region>
        <Bucket></Bucket>
        <Object></Object>
        <SpriteObject></SpriteObject>
      </Output>
      <PicProcessResult>
      </PicProcessResult>
    </Operation>
  </JobsDetail>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:--- |:--- |:--- |
| Response | None | Response container | Container |

<span id="Response"></span>
`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:--- |:--- |:--- |
| JobsDetail | Response | Job details |  Container |

<span id="jobsDetail"></span>
`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:--- |:--- |:--- |
| Code               | Response.JobsDetail | Error code, which is returned only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error message, which is returned only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Job ID                               | String    |
| Tag | Response.JobsDetail | Job type: PicProcess | String |
| State | Response.JobsDetail | Job status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. |  String |
| CreationTime | Response.JobsDetail | Job creation time |  String |
| StartTime | Response.JobsDetail | Job start time |  String |
| EndTime | Response.JobsDetail | Job end time |  String |
| QueueId            | Response.JobsDetail | Queue ID of the job                       | String    |
| Input              | Response.JobsDetail | Input resource address of the job                   | Container |
| Operation | Response.JobsDetail | Operation rule. Up to six jobs can be performed on the same file. |  Container |

`Input` has the following sub-nodes:
Same as the `Request.Input` node in the request.

<span id="Operation"></span>
`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:--- |:--- |:--- |
| TemplateId | Response.JobsDetail.Operation | Job template ID |  String |
| Output             | Response.JobsDetail.Operation | File output address               | Container |
| PicProcessResult | Response.JobsDetail.Operation | Output image information. This node will not be returned when there is no output. | Container |

`Output` has the following sub-nodes:
Same as the `Request.Operation.Output` node in the request.

`PicProcessResult` has the following sub-nodes:
Same as the `UploadResult` node in the [persistent image processing](https://intl.cloud.tencent.com/document/product/1045/33695) API.

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

**Using the image processing template ID**

#### Request

```shell
POST /pic_jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml



<Request>
  <Tag>PicProcess</Tag>
  <Input>
    <Object>test.jpg</Object>
  </Input>
  <Operation>
    <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
    <Output>
      <Region>ap-beijing</Region>
      <Bucket>abc-1250000000</Bucket>
      <Object>picprocess.jpg</Object>
      <SpriteObject></SpriteObject>
    </Output>
    <PicProcessResult>
    </PicProcessResult>
  </Operation>
  <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
  <CallBack>https://www.callback.com</CallBack>
</Request>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzh****=



<Response>
  <JobsDetail>
    <Code>Success</Code>
    <Message>Success</Message>
    <JobId>je8f65004eb8511eaaed4f377124a303c</JobId>
    <State>Submitted</State>
    <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    <EndTime></EndTime>
    <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
    <Tag>PicProcess</Tag>
    <Input>
      <Object>test.jpg</Object>
    </Input>
    <Operation>
      <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
      <Output>
        <Region>ap-beijing</Region>
        <Bucket>abc-1250000000</Bucket>
        <Object>picprocess.jpg</Object>
        <SpriteObject></SpriteObject>
      </Output>
    </Operation>
  </JobsDetail>
</Response>
```



**Using the image processing parameter**

#### Request

```shell
POST /pic_jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml



<Request>
  <Tag>PicProcess</Tag>
  <Input>
    <Object>test.jpg</Object>
  </Input>
  <Operation>
    <PicProcess>
      <IsPicInfo>true</IsPicInfo>
      <ProcessRule>imageMogr2/rotate/90</ProcessRule>
    </PicProcess>
    <Output>
      <Region>ap-beijing</Region>
      <Bucket>abc-1250000000</Bucket>
      <Object>picprocess.jpg</Object>
      <SpriteObject></SpriteObject>
    </Output>
  </Operation>
  <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
  <CallBack>https://www.callback.com</CallBack>
</Request>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzh****=



<Response>
  <JobsDetail>
    <Code>Success</Code>
    <Message>Success</Message>
    <JobId>jabcxxxxfeipplsdfwe</JobId>
    <State>Submitted</State>
    <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    <EndTime></EndTime>
    <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
    <Tag>PicProcess</Tag>
    <Input>
      <Object>test.jpg</Object>
    </Input>
    <Operation>
        <PicProcess>
          <IsPicInfo>true</IsPicInfo>
          <ProcessRule>imageMogr2/rotate/90</ProcessRule>
        </PicProcess>
        <Output>
            <Region>ap-beijing</Region>
            <Bucket>abc-1250000000</Bucket>
            <Object>picprocess.jpg</Object>
            <SpriteObject></SpriteObject>
        </Output>
        <PicProcessResult>
        </PicProcessResult>
    </Operation>
  </JobsDetail>
</Response>
```
