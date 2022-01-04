## Feature Description
This API (`CreateMediaTemplate`) is used to create a watermark template.

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
                API Explorer makes it easy to make online API calls, verify signatures, generate SDK code, search for APIs, etc. You can also use it to query the content of each request as well as its response.
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

>?Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609). 

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
        <Url>http://examplebucket-1250000000.ci.ap-beijing.myqcloud.com/shuiyin_2.png</Url>
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
| Response           | None     | Response container | Container |


`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Tag                | Request | Task type: Watermark                                   | String    | Yes   |
| Name               | Request | Template name. The value can contain only Chinese characters, letters, digits, underscores (_), hyphens (-), and asterisks (\*).                                             | String    | Yes   |
| Watermark           | Request| Watermark information                                              | Container | Yes   |


`Watermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------  | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Type                | Request.Watermark | Watermark type    | String    | Yes   | None  | Text: text watermark. Image: image watermark |
| Pos                 | Request.Watermark | Reference position    | String    | Yes   | None  | TopRight, TopLeft, BottomRight, BottomLeft |
| LocMode             | Request.Watermark | Offset mode    | String    | Yes   | None  | Relativity: proportionally. Absolute: fixed position |
| Dx                  | Request.Watermark | Horizontal offset    | String    | Yes   | None  | 1. Image watermark with `Background` being `true`: If `locMode` is `Relativity`, the unit is %, and the value range is [-300, 0]. If `locMode` is `Absolute`, the unit is px, and the value range is [-4096, 0]. <br/> 2. Image watermark with `Background` being `false`: If `locMode` is `Relativity`, the unit is %, and the value range is [0, 100]. If `locMode` is `Absolute`, the unit is px, and the value range is [0, 4096].<br/>3. Text watermark: If `locMode` is `Relativity`, the unit is %, and the value range is [0, 100]. If `locMode` is `Absolute`, the unit is px, and the value range is [0, 4096]. |
| Dy                  | Request.Watermark | Vertical offset    | String    | Yes   | None  | 1. Image watermark with `Background` being `true`: If `locMode` is `Relativity`, the unit is %, and the value range is [-300, 0]. If `locMode` is `Absolute`, the unit is px, and the value range is [-4096, 0]. <br/> 2. Image watermark with `Background` being `false`: If `locMode` is `Relativity`, the unit is %, and the value range is [0, 100]. If `locMode` is `Absolute`, the unit is px, and the value range is [0, 4096].<br/>3. Text watermark: If `locMode` is `Relativity`, the unit is %, and the value range is [0, 100]. If `locMode` is `Absolute`, the unit is px, and the value range is [0, 4096]. |
| StartTime           | Request.Watermark | Watermark start time | String    | No   | 0   | 1. [0, Video duration] <br/> 2. Unit: second <br/> 3. Supports the float format, accurate to milliseconds. |
| EndTime             | Request.Watermark | Watermark end time | String    | No   | Video end time  | 1. [0, Video duration] <br/> 2. Unit: second <br/> 3. Supports the float format, accurate to milliseconds. |
| Image               | Request.Watermark | Image watermark node | Container    | No   | None  | None |
| Text                | Request.Watermark | Text watermark node | Container    | No   | None  | None |


`Image` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------  | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Url                 | Request.Watermark.<br/>Image | Watermark image address (The URL must be encoded before being passed in.)   | String    | Yes   | None  | Same as the watermark image address of the bucket. |
| Mode                 | Request.Watermark.<br/>Image | Dimension mode    | String    | Yes   | None   | 1. Original: original size <br/>  2. Proportion: scaled proportionally <br/> 3. Fixed: fixed size |
| Width                | Request.Watermark.<br/>Image | Width         | String    | No   | None   | 1. If `Mode` is `Original`, the watermark image width cannot be set. <br/> 2. If `Mode` is `Proportion`, the unit is %, and the value range is [100, 300] for the background image and [1, 100] for the foreground image. Compared with the video width, the watermark image width cannot be greater than 4096 px. <br/>3. If `Mode` is `Fixed`, the unit is px, and the value range is [8, 4096].<br/> 4. If only `Width` is set, `Height` is calculated according to the original watermark image proportion.<br/> |
| Height               | Request.Watermark.<br/>Image | Height         | String    | No   | None   | 1. If `Mode` is `Original`, the watermark image height cannot be set. <br/> 2. If `Mode` is `Proportion`, the unit is %, and the value range is [100, 300] for the background image and [1, 100] for the foreground image. Compared with the video height, the watermark image height cannot be greater than 4096 px. <br/>3. If `Mode` is `Fixed`, the unit is px, and the value range is [8, 4096].<br/> 4. If only `Height` is set, `Width` is calculated according to the original watermark image proportion.<br/>|
| Transparency         | Request.Watermark.<br/>Image | Transparency      | String    | Yes   | None   | Value range: [1, 100]. Unit: % |
| Background           | Request.Watermark.<br/>Image | Whether it is a background image   | String    | No   | false   | true, false |

Watermark position description:
![](https://qcloudimg.tencent-cloud.cn/raw/29d64bf9e710bfca509f10c62bc5ff92.png)

`Text` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------  | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| FontSize            | Request.Watermark.<br/>Text | Font size     | String    | Yes   | None  | Value range: [5, 100]; unit: px |
| FontType            | Request.Watermark.<br/>Text | Font type    | String    | Yes   | None  | See the table below. |
| FontColor           | Request.Watermark.<br/>Text | Font color    | String    | Yes   | None  | Format: 0xRRGGBB |
| Transparency        | Request.Watermark.<br/>Text | Transparency      | String    | Yes   | None  | Value range: [1, 100]. Unit: %|
| Text                | Request.Watermark.<br/>Text | Watermark content    | String    | Yes   | None  | The value can be up to 64 characters in length and contain only Chinese characters, letters, digits, underscores (_), hyphens (-), and asterisks (*). |



`FontType` has the following sub-nodes:

| Font Name               | Supported Language             | Description
| ------------------     | -------                | ------
| simfang.ttf            |  Chinese/English                 | FangSong
| simhei.ttf             |  Chinese/English                 | SimHei
| simkai.ttf             |  Chinese/English                 | KaiTi
| simsun.ttc             |  Chinese/English                 | SimSun
| STHeiti-Light.ttc      |  Chinese/English                 | STHeiti-Light
| STHeiti-Medium.ttc     |  Chinese/English                 | STHeiti-Medium
| youyuan.TTF            |  Chinese/English                 | YouYuan
| ariblk.ttf             |  English                    | None
| arial.ttf              |  English                    | None
| ahronbd.ttf            |  English                    | None
| Helvetica.dfont        |  English                    | None
| HelveticaNeue.dfont    |  English                    | None


## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
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
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :----------------------------------------------------- | :-------- |
| Response           | None     | Response container | Container |


`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------- | :-------- |
| TemplateId          | Response | Template ID                   | String    |
| Watermark           | Response| Watermark information. Same as `Watermark` in the request body. | Container |




#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Examples

#### Request 1 (text watermark)

```shell
POST /template HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
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
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****



<Response>
    <Template>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
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
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
   </Template>
</Response>
```

#### Request 2 (image watermark)

```shell
POST /template HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
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
        <Url>http://examplebucket-1250000000.ci.ap-beijing.myqcloud.com/shuiyin_2.png</Url>
        <Mode>Proportion</Mode>
        <Width>10</Width>
        <Height>10</Height>
        <Transparency>30</Transparency>
      </Image>
   </Watermark>
</Request>
```

### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****



<Response>
    <Template>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
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
                <Url>http://examplebucket-1250000000.ci.ap-beijing.myqcloud.com/shuiyin_2.png</Url>
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
