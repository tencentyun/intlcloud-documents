## Feature Description

This API is used to create a watermark template.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateWatermarkTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
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
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
>

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609). 

#### Request body

This request requires the following request body:

```shell
<Request>
    <Tag>Watermark</Tag>
    <Name>TemplateName</Name>
    <Watermark>
        <Type>Text</Type>
        <LocMode>Absolute</LocMode>
        <Dx>128</Dx>
        <Dy>128</Dy>
        <Pos>TopRight</Pos>
        <StartTime>0</StartTime>
        <EndTime>100.5</EndTime>
        <Text>
            <Text>Watermark content</Text>
            <FontSize>30</FontSize>
            <FontType></FontType>
            <FontColor>0xRRGGBB</FontColor>
            <Transparency>30</Transparency>
        </Text>
    </Watermark>
</Request>

<Request>
    <Tag>Watermark</Tag>
    <Name>TemplateName</Name>
    <Watermark>
        <Type>Image</Type>
        <LocMode>Absolute</LocMode>
        <Dx>128</Dx>
        <Dy>128</Dy>
        <Pos>TopRight</Pos>
        <StartTime>0</StartTime>
        <EndTime>100.5</EndTime>
        <Image>
            <Url>http://test-1234567890.ci.ap-beijing.myqcloud.com/shuiyin_2.png</Url>
            <Mode>Proportion</Mode>
            <Width>10</Width>
            <Height></Height>
            <Transparency>100</Transparency>
        </Image>
    </Watermark>
</Request>

```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Request            | None     | Request container | Container |

<span id="Request"></span>
`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------- | --------- | ---- |
| Tag                | Request | Template type: Watermark                                   | String    | Yes   |
| Name               | Request | Template name, which can contain letters, digits, underscores (_), hyphens (-), and asterisks (\*). | String    | Yes       |
| Watermark           | Request | Watermark information                                              | Container | Yes   |

<span id="Watermark"></span>
`Watermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | ---- | ------------ | ------------------------------------------------------------ |
| Type                | Request.Watermark | Watermark type    | String    | Yes   | None  | Text: Text watermark. Image: Image watermark. |
| Pos                 | Request.Watermark | Reference position    | String    | Yes   | None  | TopRight, TopLeft, BottomRight, BottomLeft, Left, Right, Top, Bottom, Center     |
| LocMode             | Request.Watermark | Offset mode    | String    | Yes   | None  | Relativity: Proportionally. Absolute: Fixed position. |
| Dx                  | Request.Watermark | Horizontal offset    | String    | Yes   | None  | 1. Image watermark with `Background` being `true`: If `locMode` is `Relativity`, the unit is %, and the value range is [-300, 0]. If `locMode` is `Absolute`, the unit is px, and the value range is [-4096, 0]. <br/> 2. Image watermark with `Background` being `false`: If `locMode` is `Relativity`, the unit is %, and the value range is [0, 100]. If `locMode` is `Absolute`, the unit is px, and the value range is [0, 4096].<br/>3. Text watermark: If `locMode` is `Relativity`, the unit is %, and the value range is [0, 100]. If `locMode` is `Absolute`, the unit is px, and the value range is [0, 4096].<br/>4. If `Pos` is `Top`, `Bottom`, or `Center`, this parameter will not take effect. |
| Dy                  | Request.Watermark | Vertical offset    | String    | Yes   | None  | 1. Image watermark with `Background` being `true`: If `locMode` is `Relativity`, the unit is %, and the value range is [-300, 0]. If `locMode` is `Absolute`, the unit is px, and the value range is [-4096, 0]. <br/> 2. Image watermark with `Background` being `false`: If `locMode` is `Relativity`, the unit is %, and the value range is [0, 100]. If `locMode` is `Absolute`, the unit is px, and the value range is [0, 4096].<br/>3. Text watermark: If `locMode` is `Relativity`, the unit is %, and the value range is [0, 100]. If `locMode` is `Absolute`, the unit is px, and the value range is [0, 4096].<br/>4. If `Pos` is `Left`, `Right`, or `Center`, this parameter will not take effect. |
| StartTime           | Request.Watermark | Watermark start time | String    | No   | 0   | 1. Value range: [0, video duration] <br/> 2. Unit: Second <br/> 3. The `float` format is supported, accurate to the millisecond. |
| EndTime             | Request.Watermark | Watermark end time | String    | No   | Video end time  | 1. Value range: [0, video duration] <br/> 2. Unit: Second <br/> 3. The `float` format is supported, accurate to the millisecond. |
| SlideConfig        | Request.Watermark | Watermark sliding configuration. If this parameter is configured, the watermark offset setting will not take effect. This parameter is not supported for top speed codec/H.265 transcoding. | Container | No | None | None |
| Image               | Request.Watermark | Image watermark node | Container    | No   | None  | None |
| Text                | Request.Watermark | Text watermark node | Container    | No   | None  | None |


`SlideConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ---------------------------------- | ------------ | ------ | ---- | ------ | ------------------------------------------------------------ |
| SlideMode            | Request.Watermark.<br/>SlideConfig | Sliding mode | String | Yes | None | Default: Not enabled. `ScrollFromLeft`: Slides from left to right. If `ScrollFromLeft` is set, the `Watermark.Pos` parameter will not take effect. |
| XSlideSpeed           | Request.Watermark.<br/>SlideConfig | Horizontal sliding speed    | String    | Yes   | None  | Valid values: An integer between 0 and 10. Default value: `0`.  |
| YSlideSpeed           | Request.Watermark.<br/>SlideConfig | Vertical sliding speed    | String    | Yes   | None  | Valid values: An integer between 0 and 10. Default value: `0`.  |


`Image` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ---------------------------- | --------------------------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| Url                | Request.Watermark.<br/>Image | Watermark image address (which must be URL-encoded before being passed in).   | String    | Yes   | None  | Same as the watermark image address of the bucket. |
| Mode                 | Request.Watermark.<br/>Image | Dimension mode    | String    | Yes   | None   | 1. `Original`: Original size <br/>  2. `Proportion`: Scaled proportionally <br/> 3. `Fixed`: Fixed size |
| Width                | Request.Watermark.<br/>Image | Width         | String    | No   | None   | 1. If `Mode` is `Original`, the watermark image width cannot be set. <br/> 2. If `Mode` is `Proportion`, the unit is %, and the value range is [100, 300] for the background image and [1, 100] for the foreground image. Compared with the video width, the watermark image width cannot be greater than 4096 px. <br/>3. If `Mode` is `Fixed`, the unit is px, and the value range is [8, 4096].<br/> 4. If only `Width` is set, `Height` is calculated according to the original watermark image aspect ratio.<br/> |
| Height             | Request.Watermark.<br/>Image | Height         | String    | No   | None   | 1. If `Mode` is `Original`, the watermark image height cannot be set. <br/> 2. If `Mode` is `Proportion`, the unit is %, and the value range is [100, 300] for the background image and [1, 100] for the foreground image. Compared with the video height, the watermark image height cannot be greater than 4096 px. <br/>3. If `Mode` is `Fixed`, the unit is px, and the value range is [8, 4096].<br/> 4. If only `Height` is set, `Width` is calculated according to the original watermark image aspect ratio.<br/>|
| Transparency       | Request.Watermark.<br/>Image | Transparency      | String    | Yes   | None   | Value range: [1, 100]. Unit: % |
| Background           | Request.Watermark.<br/>Image | Whether it is a background image   | String    | No   | false   |  Valid values: `true`, `false`. |

Watermark position description:
![](https://qcloudimg.tencent-cloud.cn/raw/127404bb9ce9dbee245af9f7af115332.png)

`Text` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | --------------------------- | -------- | ------ | ---- | ------ | --------------------------------------------------- |
| FontSize            | Request.Watermark.<br/>Text | Font size    | String    | Yes   | None  | Value range: [5, 100]. Unit: px |
| FontType            | Request.Watermark.<br/>Text | Font type    | String    | Yes   | None  | See the table below. |
| FontColor           | Request.Watermark.<br/>Text | Font color    | String    | Yes   | None  | Format: 0xRRGGBB |
| Transparency       | Request.Watermark.<br/>Text | Transparency      | String    | Yes   | None   | Value range: [1, 100]. Unit: % |
| Text                | Request.Watermark.<br/>Text | Watermark content    | String    | Yes   | None  | The value can contain up to 64 letters, digits, underscores (_), hyphens (-), and asterisks (*). |



`FontType` has the following sub-nodes:

| Font Name               | Supported Language             | Description |
| ------------------- | ---------- | ---------- |
| simfang.ttf            |  Chinese/English                 | FangSong |
| simhei.ttf             |  Chinese/English                 | SimHei |
| simkai.ttf             |  Chinese/English                 | KaiTi |
| simsun.ttc             |  Chinese/English                 | SimSun |
| STHeiti-Light.ttc      |  Chinese/English                 | STHeiti-Light |
| STHeiti-Medium.ttc     |  Chinese/English                 | STHeiti-Medium |
| youyuan.TTF            |  Chinese/English                 | YouYuan |
| ariblk.ttf             |  English                    | None |
| arial.ttf              |  English                    | None |
| ahronbd.ttf            |  English                    | None |
| Helvetica.dfont        |  English                    | None |
| HelveticaNeue.dfont    |  English                    | None |


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Tag>Watermark</Tag>
        <Name>TemplateName</Name>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <Watermark>
            <Type>Text</Type>
            <LocMode>Absolute</LocMode>
            <Dx>128</Dx>
            <Dy>128</Dy>
            <Pos>TopRight</Pos>
            <StartTime>0</StartTime>
            <EndTime>100.5</EndTime>
            <Text>
                <Text>Watermark content</Text>
                <FontSize>30</FontSize>
                <FontType></FontType>
                <FontColor>0xRRGGBB</FontColor>
                <Transparency>30</Transparency>
            </Text>
        </Watermark>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

<span id="Response"></span>
`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------- | :----------------------------- | :-------- |
| TemplateId         | Response.Template | Template ID                        | String    |
| Name               | Response.Template | Template name                       | String    |
| BucketId           | Response.Template | Template bucket                 | String    |
| Category           | Response.Template | Template category: Custom or Official | String    |
| Tag                | Response.Template | Template type: VideoProcess                                       | String    |
| UpdateTime         | Response.Template | Update time                       | String    |
| CreateTime         | Response.Template | Creation time                       | String    |
| Watermark          | Response.Template     | Same as `Request.Watermark` in the request body.             | Container |


#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).

## Samples

#### Request 1: Text watermark

```shell
POST /template HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml

<Request>
   <Tag>Watermark</Tag>
   <Name>TemplateName</Name>
   <Watermark>
      <Type>Text</Type>
      <LocMode>Absolute</LocMode>
      <Dx>128</Dx>
      <Dy>128</Dy>
      <Pos>TopRight</Pos>
      <StartTime>0</StartTime>
      <EndTime>100.5</EndTime>
      <Text>
        <Text>Watermark content</Text>
        <FontSize>30</FontSize>
        <FontType></FontType>
        <FontColor>0xRRGGBB</FontColor>
        <Transparency>30</Transparency>
      </Text>
   </Watermark>
</Request>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 14 Jul 2022 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <Template>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Tag>Watermark</Tag>
        <Name>TemplateName</Name>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <Watermark>
            <Type>Text</Type>
            <LocMode>Absolute</LocMode>
            <Dx>128</Dx>
            <Dy>128</Dy>
            <Pos>TopRight</Pos>
            <StartTime>0</StartTime>
            <EndTime>100.5</EndTime>
            <Text>
                <Text>Watermark content</Text>
                <FontSize>30</FontSize>
                <FontType></FontType>
                <FontColor>0xRRGGBB</FontColor>
                <Transparency>30</Transparency>
            </Text>
        </Watermark>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
   </Template>
</Response>
```

#### Request 2: Image watermark

```shell
POST /template HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml

<Request>
   <Tag>Watermark</Tag>
   <Name>TemplateName</Name>
   <Watermark>
      <Type>Image</Type>
      <LocMode>Absolute</LocMode>
      <Dx>128</Dx>
      <Dy>128</Dy>
      <Pos>TopRight</Pos>
      <StartTime>0</StartTime>
      <EndTime>100.5</EndTime>
      <Image>
        <Url>http://test-1234567890.ci.ap-beijing.myqcloud.com/shuiyin_2.png</Url>
        <Mode>Proportion</Mode>
        <Width>10</Width>
        <Height>10</Height>
        <Transparency>30</Transparency>
      </Image>
   </Watermark>
</Request>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 14 Jul 2022 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <Template>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Tag>Watermark</Tag>
        <Name>TemplateName</Name>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <Watermark>
            <Type>Image</Type>
            <LocMode>Absolute</LocMode>
            <Dx>128</Dx>
            <Dy>128</Dy>
            <Pos>TopRight</Pos>
            <StartTime>0</StartTime>
            <EndTime>100.5</EndTime>
            <Image>
                <Url>http://test-1234567890.ci.ap-beijing.myqcloud.com/shuiyin_2.png</Url>
                <Mode>Proportion</Mode>
                <Width>10</Width>
                <Height>10</Height>
                <Transparency>30</Transparency>
            </Image>
        </Watermark>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```
