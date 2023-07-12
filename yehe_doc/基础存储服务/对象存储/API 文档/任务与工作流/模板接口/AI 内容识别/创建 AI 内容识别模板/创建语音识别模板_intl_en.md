## Feature Description

This API is used to create a speech recognition template.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateTranscodeTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
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
> - When this feature is used by a sub-account, relevant permissions must be granted.
>

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This request requires the following request body:

```shell
<Request>
    <Tag>SpeechRecognition</Tag>
    <Name>TemplateName</Name>
    <SpeechRecognition>
        <EngineModelType>16k_zh</EngineModelType>
        <ResTextFormat>1</ResTextFormat>
        <FilterDirty>0</FilterDirty>
        <FilterModal>1</FilterModal>
        <ConvertNumMode>0</ConvertNumMode>
        <SpeakerDiarization>1</SpeakerDiarization>
        <SpeakerNumber>0</SpeakerNumber>
        <FilterPunc>0</FilterPunc>
        <OutputFileType>txt</OutputFileType>
    </SpeechRecognition>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | ---- |
| Request            | None     | Request container. | Container | Yes   |

<span id="Request"></span>
`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- | ---- |
| Tag                | Request | Template tag: SpeechRecognition.                                | String    | Yes   | No |
| Name               | Request | Template name, which can contain letters, digits, underscores (_), hyphens (-), and asterisks (\*). | String    | Yes       | None                             |
| SpeechRecognition  | Request | Speech recognition parameter.                                                  | Container | Yes   | None |

<span id="SpeechRecognition"></span>
`SpeechRecognition` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | :-------------------------------------- | ------------------------------------------------------------ | ------- | -------- |
| EngineModelType    | Request.Speech<br>Recognition | Engine model type, divided into phone call and non-phone call scenarios. </br>Phone call scenarios: <ul  style="margin: 0;"><li>8k_zh: 8 kHz, for Mandarin in general scenarios (available for dual-channel audio). </li><li>8k_zh_s: 8 kHz, for Mandarin with speaker separation (available for mono-channel audio only). </li><li>8k_en: 8 kHz, for English. </li></ul>Non-phone call scenarios: <ul  style="margin: 0;"><li>16k_zh: 16 kHz, for Mandarin in general scenarios. </li><li>16k_zh_video: 16 kHz, for audio/video scenarios. </li><li>16k_en: 16 kHz, for English. </li><li>16k_ca: 16 kHz, for Cantonese. </li><li>16k_ja: 16 kHz, for Japanese. </li><li>16k_zh_edu: For Mandarin in education scenarios. </li><li>16k_en_edu: For English in education scenarios. </li><li>16k_zh_medical: For healthcare scenarios. </li><li>16k_th: For Thai. </li><li>16k_zh_dialect: Multi-dialect, for up to 23 dialects.</li></ul> | String  | Yes       |
| ChannelNum         | Request.Speech<br>Recognition | Number of sound channels: <ul  style="margin: 0;"><li>1: Mono. If `EngineModelType` is not the phone call scenario, only mono channel is supported. </li><li>2: Dual (for the 8k_zh engine only, where the two channels correspond to the caller and callee respectively). </li></ul> | Integer | Yes |
| ResTextFormat      | Request.Speech</br>Recognition | Format of the returned recognition result. <ul  style="margin: 0;"><li>0: Recognition result text, including the list of segment timestamps. </li><li>1: Detailed word-level recognition result, excluding punctuation marks but including the speech speed value (the list of word timestamps, generally used to generate subtitles). </li><li>2: Detailed word-level recognition result, including punctuation marks and the speech speed value. </li></ul> | Integer | Yes       |
| FilterDirty        | Request.Speech</br>Recognition | Whether to filter restricted words (for the Mandarin engine only). <ul  style="margin: 0;"><li>0: Does not filter. </li><li>1: Filters. </li><li>2: Replaces restricted words with `*`. </li><li>Default value: `0`. </li></ul>| Integer | No       |
| FilterModal        | Request.Speech<br>Recognition | Whether to filter modal particles (for the Mandarin engine only). <ul  style="margin: 0;"><li>0: Does not filter. </li><li>1: Filters partially. </li><li>2: Filters strictly. </li><li>Default value: `0`.</li></ul>  | Integer | No       |
| ConvertNumMode     | Request.Speech<br>Recognition | Whether to intelligently convert Chinese numbers to Arabic numerals (for the Mandarin engine only): <ul  style="margin: 0;"><li>0: Directly outputs Chinese numbers. </li><li>1: Intelligently converts based on the scenario. </li><li>3: Enables mathematic number conversion. </li><li>Default value: `0`.</li></ul>  | Integer | No       |
| SpeakerDiarization | Request.Speech</br>Recognition | Whether to enable speaker separation: <ul  style="margin: 0;"><li>0: No. </li><li>1: Yes (for mono-channel audios with the 8k_zh, 16k_zh, or 16k_zh_video engine only). </li><li>Default value: `0`. </li><li>Note: In the 8 kHz phone call scenario, we recommend you use dual channels to distinguish between the caller and callee by setting `ChannelNum=2`, so you don't need to enable speaker separation. </li></ul> | Integer | No      |
| SpeakerNumber      | Request.Speech</br>Recognition | Number of speakers to be separated (with speaker separation enabled). Value range: 0–10. <br><li>0: Automatic separation (currently only for six or fewer people only). 1–10: Specified number of speakers to be separated. Default value: `0`. | Integer | No |
| FilterPunc         | Request.Speech</br>Recognition | Whether to filter punctuation marks (currently for the Mandarin engine only): <ul  style="margin: 0;"><li>0: Does not filter. </li><li>1: Filters the punctuation mark at the end of the sentence. </li><li>2: Filters all punctuation marks. </li><li>Default value: `0`. </li></ul> | Integer | No |
| OutputFileType     | Request.Speech</br>Recognition | Output file type. Valid values: `txt`, `srt`. Default value: `txt`. | String | No       |


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <Tag>SpeechRecognition</Tag>
        <Name>TemplateName</Name>
        <State>Normal</State>
        <Tag>SpeechRecognition</Tag>
        <CreateTime></CreateTime>
        <UpdateTime></UpdateTime>
        <BucketId></BucketId>
        <Category>Custom</Category>
        <SpeechRecognition>
            <EngineModelType>16k_zh</EngineModelType>
            <ResTextFormat>1</ResTextFormat>
            <FilterDirty>0</FilterDirty>
            <FilterModal>1</FilterModal>
            <ConvertNumMode>0</ConvertNumMode>
            <SpeakerDiarization>1</SpeakerDiarization>
            <SpeakerNumber>0</SpeakerNumber>
            <FilterPunc>0</FilterPunc>
            <OutputFileType>txt</OutputFileType>
        </SpeechRecognition>
    </Template>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :----------------------------------------------------- | :-------- |
| Response           | None     | Response container | Container |

<span id="Response"></span>
`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------------- | :----------------------------------------------------------- | :-------- |
| TemplateId         | Response.Template     | Template ID.                                                      | String    |
| Name               | Response.Template     | Template name.                                                     | String    |
| BucketId           | Response.Template     | Template bucket.                                                | String    |
| Category           | Response.Template     | Template category: `Custom` or `Official`.                                | String    |
| Tag                | Response.Template     | Template tag: SpeechRecognition.                                   | String    |
| UpdateTime         | Response.Template     | Update time.                                                     | String    |
| CreateTime         | Response.Template     | Creation time.                                                     | String    |
| SpeechRecognition  | Response.Template     | Same as the `Request.SpeechRecognition` in the request body.                 | Container |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).


## Samples

#### Request

```shell
POST /template HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-chongqing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml

<Request>
    <Tag>SpeechRecognition</Tag>
    <Name>TemplateName</Name>
    <SpeechRecognition>
        <EngineModelType>16k_zh</EngineModelType>
        <ResTextFormat>1</ResTextFormat>
        <FilterDirty>0</FilterDirty>
        <FilterModal>1</FilterModal>
        <ConvertNumMode>0</ConvertNumMode>
        <SpeakerDiarization>1</SpeakerDiarization>
        <SpeakerNumber>0</SpeakerNumber>
        <FilterPunc>0</FilterPunc>
        <OutputFileType>txt</OutputFileType>
    </SpeechRecognition>
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
        <Name>TemplateName</Name>
        <State>Normal</State>
        <Tag>SpeechRecognition</Tag>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <SpeechRecognition>
            <EngineModelType>16k_zh</EngineModelType>
            <ChannelNum>1</ChannelNum>
            <ResTextFormat>0</ResTextFormat>
            <FilterDirty>1</FilterDirty>
            <FilterModal>0</FilterModal>
            <ConvertNumMode>1</ConvertNumMode>
            <SpeakerDiarization>0</SpeakerDiarization>
            <SpeakerNumber>0</SpeakerNumber>
            <FilterPunc>0</FilterPunc>
        </SpeechRecognition>
    </Template>
</Response>
```
