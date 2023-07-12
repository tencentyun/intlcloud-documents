## Feature Description

This API is used to submit a super resolution job.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateAnimationTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
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
POST /jobs HTTP/1.1
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

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/49351).

#### Request body

This request requires the following request body:

```shell
<Request>
    <Tag>SuperResolution</Tag>
    <Input>
        <Object>input/demo.mp4</Object>
    </Input>
    <Operation>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <TranscodeTemplateId>t160606b9752148c4absdfaf2f55163b1f</TranscodeTemplateId>
        <WatermarkTemplateId>t146d70eb241c44c63b6efc1cc93ccfc5d</WatermarkTemplateId>
        <WatermarkTemplateId>t12a74d11687d444deba8a6cc52051ac27</WatermarkTemplateId>
        <DigitalWatermark>
            <Type>Text</Type>
            <Message>123456789ab</Message>
            <Version>V1</Version>
            <IgnoreError>false</IgnoreError>
        </DigitalWatermark>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/out.mp4</Object>
        </Output>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
    <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
    <CallBack>http://callback.demo.com</CallBack>
    <CallBackFormat>JSON<CallBackFormat>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | -------- |
| Request            | None     | Request container | Container | Yes       |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | ------------------------------- | --------- | -------- |
| Tag                | Request | Job tag: SuperResolution                            | String    | Yes   |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule                                  | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default value). It has a higher priority than that of the queue. | String | No |
| CallBackType       | Request | Job callback type, which can be `Url` (default value) or `TDMQ`. It has a higher priority than that of the queue.                    | String | No |
| CallBack           | Request | Job callback address, which has a higher priority than that of the queue. If it is set to `no`, no callbacks will be generated at the callback address of the queue. | String | No |
| CallBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure](https://intl.cloud.tencent.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |


`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | ---------- | ------ | -------- |
| Object             | Request.Input | Media filename | String | Yes   |

<span id="operation"></span>
`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------- | ----------------- | ------------------------------------------------------------ | --------- | -------- |
| SuperResolution    | Request.Operation | Super resolution template parameter. This node and `TemplateId` cannot be empty at the same time.                                         | Container | No   |
| TemplateId                   | Request.Operation | Super resolution template ID, which is used first. This node and `SuperResolution` cannot be empty at the same time.                                        | String    | No  |
| Transcode          | Request.Operation | Transcoding template parameter. This node and `TranscodeTemplateId` cannot be empty at the same time.             | Container | No   |
| TranscodeTemplateId | Request.Operation | Transcoding template ID. This node and `Transcode` cannot be empty at the same time. Use this node first.           | String  | No|
| Watermark          | Request.Operation | Watermark template parameter. Same as `Request.Watermark` in the watermark template creation API <a href="https://intl.cloud.tencent.com/document/product/1045/49917" target="_blank">CreateMediaTemplate</a>. Up to three watermarks can be passed in. | Container array | No |
| WatermarkTemplateId| Request.Operation | Watermark template ID. Up to three watermark template IDs can be passed in. If `Watermark` and `WatermarkTemplateId` exist at the same time, use `WatermarkTemplateId` first.          | String array    | No |
| DigitalWatermark   | Request.Operation | Specifies the digital watermark parameter                                                         | Container | No   |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| JobLevel            | Request.Operation | Job priority. The greater the value, the higher the priority. Valid values: `0`, `1`, `2`. Default value: `0`. | String | No |


>? To submit a super resolution job, you must pass in the transcoding parameter. For the super resolution parameter, `TemplateId` is used first, and if `TemplateId` is unavailable, `SuperResolution` is used. For the transcoding parameter, `TranscodeTemplateId` is used first, and if `TranscodeTemplateId` is unavailable, `Transcode` is used. For the watermark parameter, `WatermarkTemplateId` or `Watermark` can be used for configuration, and `WatermarkTemplateId` is used first.
>

`SuperResolution` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | :-------------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Resolution         | Request.Operation.SuperResolution | Same as `Request.Resolution` in the super resolution template creation API <a href="https://intl.cloud.tencent.com/document/product/1045/49910" target="_blank">CreateMediaTemplate</a>.    | String | Yes |
| EnableScaleUp         | Request.Operation.SuperResolution | Same as `Request.EnableScaleUp` in the super resolution template creation API <a href="https://intl.cloud.tencent.com/document/product/1045/49910" target="_blank">CreateMediaTemplate</a>.    | String | No |
| Version         | Request.Operation.SuperResolution | Same as `Request.Version` in the super resolution template creation API <a href="https://intl.cloud.tencent.com/document/product/1045/49910" target="_blank">CreateMediaTemplate</a>.    | String | No |

`Transcode` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | :------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| TimeInterval          | Request.Operation.Transcode | Same as `Request.TimeInterval` in the transcoding template creation API <a href="https://intl.cloud.tencent.com/document/product/1045/49911" target="_blank">CreateMediaTemplate</a>.    | Container | No   |
| Container          | Request.Operation.Transcode | Same as `Request.Container` in the transcoding template creation API <a href="https://intl.cloud.tencent.com/document/product/1045/49911" target="_blank">CreateMediaTemplate</a>.    | Container | No   |
| Video          | Request.Operation.Transcode | Same as `Request.Video` in the transcoding template creation API <a href="https://intl.cloud.tencent.com/document/product/1045/49911" target="_blank">CreateMediaTemplate</a>.    | Container | No   |
| Audio          | Request.Operation.Transcode | Same as `Request.Audio` in the transcoding template creation API <a href="https://intl.cloud.tencent.com/document/product/1045/49911" target="_blank">CreateMediaTemplate</a>.    | Container | No   |
| TransConfig          | Request.Operation.Transcode | Same as `Request.TransConfig` in the transcoding template creation API <a href="https://intl.cloud.tencent.com/document/product/1045/49911" target="_blank">CreateMediaTemplate</a>.    | Container | No   |
| AudioMix           | Request.Operation.Transcode     | Audio mix parameter as described in <a href="https://intl.cloud.tencent.com/document/product/1045/49945" target="_blank">Structure</a>.                                    | Container array | No |

`DigitalWatermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | :--------------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Message               | Request.Operation.DigitalWatermark |  The string embedded by the digital watermark, which can contain up to 64 letters, digits, underscores (\_), hyphens (-), and asterisks (\*).    | String | Yes   |
| Type               | Request.Operation.DigitalWatermark | Watermark type, which currently can be set to `Text` only.      | String | Yes |
| Version            | Request.Operation.DigitalWatermark | Watermark version, which currently can be set to `V1` only.       | String | Yes |
| IgnoreError        | Request.Operation.DigitalWatermark | Whether to ignore the watermarking failure and continue the job. Valid values: `true`, `false` (default value).  | string | No   |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------ | ---------------- | ------ | -------- |
| Region             | Request.Operation.Output | Bucket region | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Output result filename | String | Yes   |



## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/49352).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>j8d121820f5e411ec926ef19d53ba9c6f</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T14:44:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Tag>SuperResolution</Tag>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
              <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
              <TemplateName>superresolution_demo</TemplateName>
              <TranscodeTemplateId>t160606b9752148c4absdfaf2f55163b1f</TranscodeTemplateId>
              <WatermarkTemplateId>t146d70eb241c44c63b6efc1cc93ccfc5d</WatermarkTemplateId>
              <WatermarkTemplateId>t12a74d11687d444deba8a6cc52051ac27</WatermarkTemplateId>
              <DigitalWatermark>
                  <Type>Text</Type>
                  <Message>123456789ab</Message>
                  <State>Running</State>
                  <Version>V1</Version>
                  <IgnoreError>false</IgnoreError>
              </DigitalWatermark>
              <Output>
                  <Region>ap-chongqing</Region>
                  <Bucket>test-123456789</Bucket>
                  <Object>output/out.mp4</Object>
              </Output>
              <UserData>This is my data.</UserData>
              <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------- | :-------- |
| JobsDetail         | Response | Job details | Container |

<span id="jobsDetail"></span>
`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :-------- |
| Code               | Response.JobsDetail | Error code, which is returned only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error message, which is returned only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Job ID                               | String    |
| Tag                | Response.JobsDetail | Job tag: SuperResolution                              | String    |
| State | Response.JobsDetail | Job status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. |  String |
| CreationTime       | Response.JobsDetail | Job creation time                         | String    |
| StartTime | Response.JobsDetail | Job start time |  String |
| EndTime | Response.JobsDetail | Job end time |  String |
| QueueId            | Response.JobsDetail | ID of the queue which the job is in                       | String    |
| Input              | Response.JobsDetail | Input resource address of the job                   | Container |
| Operation          | Response.JobsDetail | Operation rule                           | Container |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------------ | ---------------- | ------ |
| Region             | Response.JobsDetail.Input | Bucket region     | String |
| Bucket             | Response.JobsDetail.Input | Result storage bucket | String |
| Object             | Response.JobsDetail.Input | Output result filename | String |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :------------------ | :---------------------------- | :----------------------------------------------------------- | :-------- |
| SuperResolution             | Response.JobsDetail.Operation | Same as `Request.Operation.SuperResolution` in the request.  | Container |
| TemplateId | Response.JobsDetail.Operation | Job template ID |  String |
| TemplateName        | Response.JobsDetail.Operation | Job template name, which will be returned if `TemplateId` exists. | String    |
| Transcode             | Response.JobsDetail.Operation | Same as `Request.Operation.Transcode` in the request.  | Container |
| TranscodeTemplateId | Response.JobsDetail.Operation | Transcoding template ID.                                                 | String    |
| Watermark             | Response.JobsDetail.Operation | Same as `Request.Operation.Watermark` in the request.  | Container array |
| WatermarkTemplateId| Response.JobsDetail.Operation | Watermark template ID.          | String array   |
| Output             | Response.JobsDetail.Operation | Same as `Request.Operation.Output` in the request.  | Container |
| MediaInfo           | Response.JobsDetail.Operation | Media information of the output file, which will not be returned when the job is not completed. | Container |
| MediaResult        | Response.JobsDetail.Operation | Basic information of the output file, which will not be returned when the job is not completed. | Container |
| DigitalWatermark   | Response.JobsDetail.Operation | Digital watermark parameter.                 | Container |
| UserData           | Response.JobsDetail.Operation | The user information passed through.                      | String |
| JobLevel    | Response.JobsDetail.Operation | Job priority                                                         | String |


`MediaInfo` has the following sub-nodes:
Same as the `Response.MediaInfo` node in the `GenerateMediaInfo` API.

`MediaResult` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | :---------------------------------- | ------------------------------------------------------------ | ------ |
| OutputFile         | Response.Operation.MediaResult | Basic information of the output file. | Container |

`OutputFile` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | :---------------------------------- | ------------------------------------------------------------ | ------ |
| Bucket             | Response.Operation.MediaResult.OutputFile | Bucket of the output file.           | String |
| Region             | Response.Operation.MediaResult.OutputFile | Bucket region of the output file.  | String |
| ObjectName         | Response.Operation.MediaResult.OutputFile | Output filename. There may be multiple values.         | String array |
| Md5Info            | Response.Operation.MediaResult.OutputFile | MD5 information of the output file. | Container array |

`Md5Info` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | :---------------------------------- | ------------------------------------------------------------ | ------ |
| ObjectName         | Response.Operation.MediaResult.OutputFile.Md5Info | Output filename.         | String |
| Md5                | Response.Operation.MediaResult.OutputFile.Md5Info | MD5 value of the output file.    | Container |

`DigitalWatermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | :---------------------------------- | ------------------------------------------------------------ | ------ |
| Message               | Response.Operation.DigitalWatermark |  The string in the digital watermark successfully embedded in the video, which can contain up to 64 letters, digits, underscores (\_), hyphens (-), and asterisks (\*).    | string |
| Type               | Response.Operation.DigitalWatermark | Watermark type, which currently can be set to `Text` only.      | String |
| Version            | Response.Operation.DigitalWatermark | Watermark version, which currently can be set to `V1` only.      | String |
| IgnoreError        | Response.Operation.DigitalWatermark | Whether to ignore the watermarking failure and continue the job. Valid values: `true`, `false` (default value).  |string |
| State        | Response.Operation.DigitalWatermark | Whether the watermark is added successfully. Valid values: `Running`, `Success`, `Failed`.  | string |


#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).

## Samples


#### Request 1. Using the super resolution template ID

```shell
POST /jobs HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Tag>SuperResolution</Tag>
    <Input>
        <Object>test.mp4</Object>
    </Input>
    <Operation>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <TranscodeTemplateId>t160606b9752148c4absdfaf2f55163b1f</TranscodeTemplateId>
        <WatermarkTemplateId>t146d70eb241c44c63b6efc1cc93ccfc5d</WatermarkTemplateId>
        <WatermarkTemplateId>t12a74d11687d444deba8a6cc52051ac27</WatermarkTemplateId>
        <DigitalWatermark>
            <Type>Text</Type>
            <Message>123456789ab</Message>
            <Version>V1</Version>
            <IgnoreError>false</IgnoreError>
        </DigitalWatermark>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/sr.mp4</Object>
        </Output>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
    <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
    <CallBack>http://callback.demo.com</CallBack>
    <CallBackFormat>JSON<CallBackFormat>
</Request>
```

#### Response 1

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Mon, 28 Jun 2022 15:23:12 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>je8f65004eb8511eaaed4f377124a303c</JobId>
        <State>Submitted</State>
        <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Tag>SuperResolution</Tag>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
            <TemplateName>superresolution_demo</TemplateName>
            <TranscodeTemplateId>t160606b9752148c4absdfaf2f55163b1f</TranscodeTemplateId>
            <WatermarkTemplateId>t146d70eb241c44c63b6efc1cc93ccfc5d</WatermarkTemplateId>
            <WatermarkTemplateId>t12a74d11687d444deba8a6cc52051ac27</WatermarkTemplateId>
            <DigitalWatermark>
                <State>Running</State>
                <Type>Text</Type>
                <Message>123456789ab</Message>
                <Version>V1</Version>
                <IgnoreError>false</IgnoreError>
            </DigitalWatermark>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>output/sr.mp4</Object>
            </Output>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```


#### Request 2. Using the super resolution processing parameter

```shell
POST /jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Tag>SuperResolution</Tag>
    <Input>
        <Object>test.mp4</Object>
    </Input>
    <Operation>
        <SuperResolution>
            <Resolution>sdtohd</Resolution>
            <EnableScaleUp>true</EnableScaleUp>
            <Version>Enhance</Version>
        </SuperResolution>
        <Transcode>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H.264</Codec>
                <Profile>high</Profile>
                <Bitrate>1000</Bitrate>
                <Width>1280</Width>
                <Fps>30</Fps>
                <Preset>medium</Preset>
            </Video>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>128</Bitrate>
                <Channels>4</Channels>
            </Audio>
            <TransConfig>
                <AdjDarMethod>scale</AdjDarMethod>
                <IsCheckReso>false</IsCheckReso>
                <ResoAdjMethod>1</ResoAdjMethod>
            </TransConfig>
            <TimeInterval>
                <Start>0</Start>
                <Duration>60</Duration>
            </TimeInterval>
        </Transcode>
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
                <FontType>simfang.ttf</FontType>
                <FontColor>0xRRGGBB</FontColor>
                <Transparency>30</Transparency>
            </Text>
        </Watermark>
        <DigitalWatermark>
            <Type>Text</Type>
            <Message>123456789ab</Message>
            <Version>V1</Version>
            <IgnoreError>false</IgnoreError>
        </DigitalWatermark>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/sr.mp4</Object>
        </Output>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
    <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
    <CallBack>http://callback.demo.com</CallBack>
    <CallBackFormat>JSON<CallBackFormat>
</Request>
```

#### Response 2

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Mon, 28 Jun 2022 15:23:12 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>je8f65004eb8511eaaed4f377124a303c</JobId>
        <State>Submitted</State>
        <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Tag>SuperResolution</Tag>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <SuperResolution>
                <Resolution>sdtohd</Resolution>
                <EnableScaleUp>true</EnableScaleUp>
                <Version>Enhance</Version>
            </SuperResolution>
            <Transcode>
                <Container>
                    <Format>mp4</Format>
                </Container>
                <Video>
                    <Codec>H.264</Codec>
                    <Profile>high</Profile>
                    <Bitrate>1000</Bitrate>
                    <Width>1280</Width>
                    <Fps>30</Fps>
                    <Preset>medium</Preset>
                </Video>
                <Audio>
                    <Codec>aac</Codec>
                    <Samplerate>44100</Samplerate>
                    <Bitrate>128</Bitrate>
                    <Channels>4</Channels>
                </Audio>
                <TransConfig>
                    <AdjDarMethod>scale</AdjDarMethod>
                    <IsCheckReso>false</IsCheckReso>
                    <ResoAdjMethod>1</ResoAdjMethod>
                </TransConfig>
                <TimeInterval>
                    <Start>0</Start>
                    <Duration>60</Duration>
                </TimeInterval>
            </Transcode>
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
                    <FontType>simfang.ttf</FontType>
                    <FontColor>0xRRGGBB</FontColor>
                    <Transparency>30</Transparency>
                </Text>
            </Watermark>
            <DigitalWatermark>
                <State>Running</State>
                <Type>Text</Type>
                <Message>123456789ab</Message>
                <Version>V1</Version>
                <IgnoreError>false</IgnoreError>
            </DigitalWatermark>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>output/sr.mp4</Object>
            </Output>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```
