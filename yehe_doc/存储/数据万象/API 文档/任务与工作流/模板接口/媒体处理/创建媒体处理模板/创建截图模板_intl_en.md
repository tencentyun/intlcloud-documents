## Feature Description
This API (`CreateMediaTemplate`) is used to create a screenshot template.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateSnapshotTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer provides various capabilities such as online call, signature verification, SDK code generation, and quick API search. You can also use it to query the request and response of each API call as well as generate sample code for calls.
            </div>
        </div>
    </div>
</div>


## Request

#### Sample request

```shell
POST /template HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see Authorization Granularity.
> 

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609). 

#### Request body
This request requires the following request body:

```shell
<Request>
   <Tag>Snapshot</Tag>
   <Name>TemplateName</Name>
   <Snapshot>
      <Mode>Interval</Mode>
      <Width>1280</Width>
      <Height></Height>
      <Start>0</Start>
      <TimeInterval></TimeInterval>
      <Count></Count>
      <SnapshotOutMode>OnlySnapshot</SnapshotOutMode>
      <SpriteSnapshotConfig>
        <CellHeight></CellHeight>
        <CellWidth></CellWidth>
        <Color></Color>
        <Columns></Columns>
        <Lines></Lines>
        <Margin><Margin/>
        <Padding><Padding/>
      </SpriteSnapshotConfig>
   </Snapshot>
</Request>

```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | ---- |
| Request            | None     | Request container | Container | Yes   |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Tag                | Request | Template type: Snapshot                                    | String    | Yes   |
| Name               | Request | Template name, which can contain letters, digits, underscores (_), hyphens (-), and asterisks (*).                   | String    | Yes   |
| Snapshot           | Request | Screenshot                                                  | Container | Yes   |


`Snapshot` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Mode                | Request.Snapshot | Screenshot mode | String    | No   | Interval | <li>Valid values: {Interval, Average, KeyFrame}</li><li>Interval: Interval mode Average: Average mode</li><li> KeyFrame: Keyframe mode</li><li> Interval mode: The `Start`, `TimeInterval`, and `Count` parameters are valid. If `Count` is set and `TimeInterval` is not set, all frames will be captured, and the total number of images captured is specified by `Count`.</li><li>Average mode: The `Start` and `Count` parameters are valid, indicating to capture a total of `Count` images at an average interval from `Start` to the end of the video.</li>|
| Start                | Request.Snapshot | Start time | String    | No   | 0 | <li>[0, video duration] </li><li>Unit: second </li><li>Supports the float format, accurate to the millisecond.</li> |
| TimeInterval         | Request.Snapshot | Screenshot time interval | String    | No   | None  | <li>(0, 3600] </li><li>Unit: second </li><li>Supports the float format, accurate to the millisecond.</li> |
| Count                | Request.Snapshot | Number of screenshots | String    | Yes   | None  | (0, 10000] |
| Width                | Request.Snapshot | Width | String    | No   |  Original video width | <li>Value range: [128, 4096]</li><li>Unit: px</li><li>If only `Width` is set, `Height` is calculated according to the original video aspect ratio. </li>|
| Height                | Request.Snapshot | Height | String    | No  | Original video height  | <li>Value range: [128, 4096]</li><li>Unit: px</li><li>If only `Height` is set, `Width` is calculated according to the original video aspect ratio.</li> |
| CIParam              | Request.Snapshot | Screenshot processing parameter  | String    | No  | None  | <li>See [Scaling](https://intl.cloud.tencent.com/document/product/1045/33713).</li><li>Example: imageMogr2/format/png |
| IsCheckCount         | Request.Snapshot | Whether to force check the number of screenshots | String    | No   | false  | <li>When the custom interval mode is used to take screenshots, if the video is not long enough to take `Count` screenshots, the average mode can be switched to for taking `Count` screenshots. |
| IsCheckBlack         | Request.Snapshot | Whether to enable black screen check | String    | No   | false  | true/false |
| BlackLevel           | Request.Snapshot | Screenshot black screen check parameter  | String    | No   | None  | <li>Valid when `IsCheckBlack` is `true`.</li><li>Value range: [30,100], indicating the proportion of black pixels. The smaller the value, the smaller the proportion of black.</li><li> If `Start` is > 0, this parameter doesn't work, and black screen will not be checked.</li><li>If `Start` is 0, this parameter is valid, and frame capturing will start from the first non-black frame.  |
| PixelBlackThreshold  | Request.Snapshot | Screenshot black screen check parameter  | String    | No   | None  | <li>Valid when `IsCheckBlack` is `true`.</li><li>The threshold to determine whether a pixel is black. Value range: [0, 255].  |
| SnapshotOutMode      | Request.Snapshot | Screenshot output mode parameter  | String    | No   | OnlySnapshot  | <li>Valid values: {OnlySnapshot, OnlySprite, SnapshotAndSprite}</li><li>OnlySnapshot: Outputs screenshots only. OnlySprite: Outputs image sprites only. SnapshotAndSprite: Outputs screenshots and image sprites. |
| SpriteSnapshotConfig | Request.Snapshot | Image sprite output configuration    | Container | No   | None  | None |


`Snapshot.SpriteSnapshotConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| CellWidth          | Request.Snapshot.SpriteSnapshotConfig | Subimage width | String    | No   | Screenshot width | <li>Value range: [8, 4096]</li><li>Unit: px |
| CellHeight          | Request.Snapshot.SpriteSnapshotConfig | Subimage height | String    | No   | Screenshot height | <li>Value range: [8, 4096]</li><li>Unit: px |
| Padding            | Request.Snapshot.SpriteSnapshotConfig | Image sprite padding size  | String    | No   | 0  | <li>Value range: [0, 1024]</li><li>Unit: px |
| Margin             | Request.Snapshot.SpriteSnapshotConfig | Image sprite margin size  | String    | No   | 0  | <li>Value range: [0, 1024]</li><li>Unit: px |
| Color              | Request.Snapshot.SpriteSnapshotConfig | Background color  | String    | Yes   | None  | For supported colors, see [2.7 Color](https://www.ffmpeg.org/ffmpeg-utils.html#color-syntax). |
| Columns            | Request.Snapshot.SpriteSnapshotConfig | Number of columns in the image sprite  | String    | Yes   | 0  | Value range: [1, 10000] |
| Lines              | Request.Snapshot.SpriteSnapshotConfig | Number of rows in the image sprite  | String    | Yes   | 0  | Value range: [1, 10000] |


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

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
            <SnapshotOutMode>OnlySnapshot</SnapshotOutMode>
            <SpriteSnapshotConfig>
              <CellHeight></CellHeight>
              <CellWidth></CellWidth>
              <Color></Color>
              <Columns></Columns>
              <Lines></Lines>
              <Margin><Margin/>
              <Padding><Padding/>
            </SpriteSnapshotConfig>
        </Snapshot>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :----------------------------------------------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------------- | :----------------------------------------------------------- | :-------- |
| Tag                | Response | Template type: Snapshot                                           | String    |
| Name               | Response | Template name                                                     | String    |
| TemplateId         | Response | Template ID                                                      | String    |
| UpdateTime         | Response | Update time                                                     | String    |
| CreateTime         | Response | Creation time                                                     | String    |
| Snapshot           | Response | Template parameters. Same as `Snapshot` in the request body.  | Container |


#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Request

```shell
POST /template HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml



<Request>
   <Tag>Snapshot</Tag>
   <Name>TemplateName</Name>
   <Snapshot>
      <Width>1280</Width>
      <Height></Height>
      <Start>0</Start>
      <TimeInterval></TimeInterval>
      <Count></Count>
      <SnapshotOutMode>OnlySnapshot</SnapshotOutMode>
      <SpriteSnapshotConfig>
        <CellHeight>128</CellHeight>
        <CellWidth>128</CellWidth>
        <Color>White</Color>
        <Columns>10</Columns>
        <Lines>10</Lines>
        <Margin>0<Margin/>
        <Padding>0<Padding/>
      </SpriteSnapshotConfig>
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
            <SnapshotOutMode>OnlySnapshot</SnapshotOutMode>
            <SpriteSnapshotConfig>
              <CellHeight>128</CellHeight>
              <CellWidth>128</CellWidth>
              <Color>White</Color>
              <Columns>10</Columns>
              <Lines>10</Lines>
              <Margin>0<Margin/>
              <Padding>0<Padding/>
            </SpriteSnapshotConfig>
        </Snapshot>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```
