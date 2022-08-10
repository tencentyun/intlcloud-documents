## Feature Description

This API (`UpdateMediaTemplate`) is used to update a screenshot template.

## Request

#### Sample request

```shell
PUT /template/<TemplateId> HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>?Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)


#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body
This request requires the following request body:

```shell
<Request>
   <Tag>Snapshot</Tag>
   <Name>TemplateName</Name>
   <TemplateId></TemplateId>
   <Snapshot>
      <Width>1280</Width>
      <Height></Height>
      <Start>0</Start>
      <TimeInterval></TimeInterval>
      <Count></Count>
   </Snapshot>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :---------------------------------------- | :-------- | ---- |
| Request            | None | Request container | Container | Yes   |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Tag                | Request | Task type: Snapshot                                    | String    | Yes   |
| Name               | Request | Template name. The value can contain only Chinese characters, letters, digits, underscores (_), hyphens (-), and asterisks (*).                   | String    | Yes   |
| Snapshot           | Request | Screenshot                                                  | Container | No   |

`Snapshot` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Mode                | Request.Snapshot | Screenshot mode | String    | Yes   | Interval | <li>Value range: {Interval, Average}</li><li>Interval, Average</li><li> Interval mode: the `Start`, `TimeInterval`, and `Count` parameters are valid. If `Count` is set and `TimeInterval` is not set, all frames will be captured, and the total number of images captured is specified by `Count`.</li><li>Average mode: the `Start` and `Count` parameters are valid, indicating that, from `Start` to the end of the video, capture a total of `Count` images at an average interval.</li>|
| Start                | Request.Snapshot | Start time | String    | Yes   | 0 | <li>[0, Video duration] </li><li>Unit: seconds </li><li>Supports the float format, accurate to milliseconds. |
| TimeInterval         | Request.Snapshot | Screenshot time interval | String    | No   | None  | <li>(0, 3600] </li><li>Unit: seconds </li><li>Supports the float format, accurate to milliseconds.</li> |
| Count                | Request.Snapshot | Number of screenshots | String    | Yes   | None  | (0, 10000] |
| Width                | Request.Snapshot | Width | String    | No   |  Original video width | <li>Value range: [128, 4096]</li><li>Unit: px</li><li>If only `Width` is set, `Height` is calculated according to the original video proportion.</li> |
| Height                | Request.Snapshot | Height | String    | No  | Original video height  | <li>Value range: [128, 4096]</li><li>Unit: px</li><li>If only `Height` is set, `Width` is calculated according to the original video proportion.</li>|


## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell

<Response>
    <Template>
        <Tag>Snapshot</Tag>
        <Name>TemplateName</Name>
        <TemplateId></TemplateId>
        <Snapshot>
            <Width>1280</Width>
            <Height></Height>
            <Start>0</Start>
            <TimeInterval></TimeInterval>
            <Count></Count>
        </Snapshot>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :----------------------------------------- | :-------- |
| Response           | None     | Response container | Container |


`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------------- | :----------------------------------------------------------- | :-------- |
| Tag                | Response | Task type: Snapshot                                           | String    |
| Name               | Response | Template name                                                     | String    |
| TemplateId         | Response | Template ID                                                      | String    |
| UpdateTime         | Response | Update time                                                     | String    |
| CreateTime         | Response | Creation time                                                     | String    |
| Snapshot           | Response | Template parameters. Same as `Snapshot` in the request body. | Container |

#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Examples

#### Request

```shell
PUT /template/<TemplateId> HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml



<Request>
   <Tag>Snapshot</Tag>
   <Name>TemplateName</Name>
   <TemplateId></TemplateId>
   <Snapshot>
      <Width>1280</Width>
      <Height></Height>
      <Start>0</Start>
      <TimeInterval></TimeInterval>
      <Count></Count>
   </Snapshot>
</Request>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzh****=



<Response>
    <Template>
        <Tag>Snapshot</Tag>
        <Name>TemplateName</Name>
        <TemplateId></TemplateId>
        <Snapshot>
            <Width>1280</Width>
            <Height></Height>
            <Start>0</Start>
            <TimeInterval></TimeInterval>
            <Count></Count>
        </Snapshot>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```
