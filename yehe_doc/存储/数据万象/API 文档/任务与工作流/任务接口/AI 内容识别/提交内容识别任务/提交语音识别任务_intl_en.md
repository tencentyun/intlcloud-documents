## Overview

This API is used to submit a speech recognition job.
>?For constraints on speech recognition, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/1045/33425).

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateAnimationTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer makes it easy for you to make online API calls, verify signatures, generate SDK code, and search for APIs. You can use it to query the request and response of each API call and generate sample SDK codes for the call.
            </div>
        </div>
    </div>
</div>



## Request

#### Sample request

```shell
POST /asr_jobs HTTP/1.1
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

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```shell
<Request>
    <Tag>SpeechRecognition</Tag>
    <Input>
        <Object>input/test.mp3</Object>
        <Url></Url>
    </Input>
    <Operation>
        <SpeechRecognition>
            <EngineModelType>16k_zh_video</EngineModelType>
            <ChannelNum>1</ChannelNum>
            <FilterDirty>1</ChannelNum>
            <FilterModal>1</ChannelNum>
        </SpeechRecognition>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/asr.txt</Object>
        </Output>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
    <QueueId>pcd463e1467964d39ad2d3f66aacd8199</QueueId>
    <CallBack>http://callback.demo.com</CallBack>
    <CallBackFormat>JSON<CallBackFormat>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | ---- |
| Request            | None     | Request container | Container | Yes   |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Tag                | Request     | Job type: SpeechRecognition.                                     | String  | Yes       |
| Input              | Request | Information about the object to be operated                                         | Container | Yes   |
| Operation          | Request | Operation rule                                  | Container | Yes   |
| QueueId            | Request | ID of the queue where the job is in                                         | String    | Yes   |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default). It has a higher priority than that of the queue. | String | No |
| CallBackType       | Request | Job callback type, which can be `Url` (default) or `TDMQ`. It has a higher priority than that of the queue.                    | String | No |
| CallBack           | Request | Job callback address, which has a higher priority than that of the queue. If it is set to `no`, no callbacks will be generated at the callback address of the queue. | String | No |
| CallBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure > CallBackMqConfig](https://intl.cloud.tencent.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|-----------| ------------- |--| ------ | ---- |
| Object             | Request.Input | Media filename | String | No   |
| Url       | Request.Input | URL that supports downloading over the public network. At least one of `Url` and `Object` must be passed in. If both parameters are passed in, `Object` is preferred. | String | No   |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | ---- |
| SpeechRecognition  | Request.Operation | Speech recognition parameter                                                  | Container | Yes   |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| JobLevel            | Request.Operation | Job priority. The greater the value, the higher the priority. Valid values: `0`, `1`, `2`. Default value: `0`. | String | No |

`SpeechRecognition` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | :-------------------------- | ----------------------------------------- | --------- | -------- |
| EngineModelType    | Request.Operation.Speech<br>Recognition | Engine model type.<br>Phone call scenario: <ul  style="margin: 0;"><li>`8k_zh`: 8 kHz Mandarin for general fields (applied to dual-channel audios)</li><li>`8k_zh_s`: 8 kHz Mandarin for speaker diarization (applied only to mono-channel audios)</li></ul>Non-phone call scenario: <ul  style="margin: 0;"><li>`16k_zh`: 16 kHz Mandarin for general fields</li><li>`16k_zh_video`: 16 kHz Mandarin for audiovisual fields</li><li>`16k_en`: 16 kHz English</li><li>`16k_ca`: 16 kHz Cantonese</li></ul>   | String | Yes       |
| ChannelNum         | Request.Operation.Speech<br>Recognition | Number of sound channels: <ul  style="margin: 0;"><li>`1`: Mono</li><li>`2`: Dual (for the 8k_zh engine only)</li></ul> | Integer | Yes |
| ResTextFormat       | Request.Operation.Speech<br>Recognition | Format of the returned recognition result.<ul  style="margin: 0;"><li>`0`: recognition result text, including the list of segment timestamps </li><li>`1`: recognition result details, including the list of word timestamps (generally used to generate subtitles and for the 16 kHz Mandarin engine only).</li></ul> | Integer | Yes       |
| FilterDirty        | Request.Operation.Speech<br>Recognition | Whether to filter restricted words (for the Mandarin engine only). <ul  style="margin: 0;"><li>`0`: Does not filter. </li><li>`1`: Filters. </li><li>`2`: Replaces restricted words with `*`. Default value: `0`. </li></ul>| Integer | No       |
| FilterModal        | Request.Operation.Speech<br>Recognition | Whether to filter modal particles (for the Mandarin engine only). <ul  style="margin: 0;"><li>`0`: Does not filter. </li><li>`1`: Filters partially. </li><li>`2`: Filters strictly. Default value: `0`.</li></ul>  | Integer | No       |
| ConvertNumMode     | Request.Operation.Speech<br>Recognition | Whether to intelligently convert Chinese numbers to Arabic numerals (for the Mandarin engine only): <ul  style="margin: 0;"><li>`0`: Directly outputs Chinese numbers. </li><li>`1`: Intelligently converts based on the scenario. Default value: `1`.</li></ul>  | Integer | No       |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------ | ------------------------------------------------------------ | ------ | -------- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Result file name                                             | String | Yes   |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

``` shell
<Response>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2021-08-05T15:43:50+0800</CreationTime>
        <EndTime>-</EndTime>
        <Input>
            <BucketId>test-1234567890</BucketId>
            <Object>input/test.mp3</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>s58ccb634149211ed84ce2b1cd7fbb14a</JobId>
        <Message/>
        <Operation>
            <JobLevel>0</JobLevel>
            <Output>
                <Bucket>test-1234567890</Bucket>
                <Object>output/asr.txt</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <SpeechRecognition>
                <ChannelNum>1</ChannelNum>
                <ConvertNumMode>0</ConvertNumMode>
                <EngineModelType>16k_zh_video</EngineModelType>
                <FilterDirty>0</FilterDirty>
                <FilterModal>0</FilterModal>
                <FilterPunc>0</FilterPunc>
                <OutputFileType>txt</OutputFileType>
                <ResTextFormat>0</ResTextFormat>
                <SpeakerDiarization>0</SpeakerDiarization>
                <SpeakerNumber>0</SpeakerNumber>
            </SpeechRecognition>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
        <QueueId>pcd463e1467964d39ad2d3f66aacd8199</QueueId>
        <StartTime>-</StartTime>
        <State>Submitted</State>
        <Tag>SpeechRecognition</Tag>
    </JobsDetail>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Result storage container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------- | :-------- |
| JobsDetail | Response | Job details |  Container |

<span id="jobsDetail"></span>
`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :-------- |
| Code               | Response.JobsDetail | Error code, which is returned only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error message, which is returned only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Job ID                               | String    |
| Tag | Response.JobsDetail | Job type: SpeechRecognition | String |
| State | Response.JobsDetail | Job status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. |  String |
| CreationTime       | Response.JobsDetail | Job creation time                         | String    |
| StartTime          | Response.JobsDetail | Job start time                                               | String    |
| EndTime          | Response.JobsDetail | Job end time                                               | String    |
| QueueId            | Response.JobsDetail | ID of the queue where the job is in                                             | String    |
| Input              | Response.JobsDetail | Same as the `Request.Input` node in the request                              | Container |
| Operation          | Response.JobsDetail | Operation rule. Up to 6 operation rules are supported.                           | Container |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :------------------ | :---------------------------- | :----------------------------------------------------------- | :-------- |
| SpeechRecognition | Response.JobsDetail.Operation | Same as `Request.Operation.SpeechRecognition` in the request.  | Container |
| Output | Response.JobsDetail.Operation | Same as `Request.Operation.Output` in the request. |  Container |
| UserData           | Response.JobsDetail.Operation | The user information passed through.                      | String |
| JobLevel    | Response.JobsDetail.Operation | Job priority                                                         | String |
| SpeechRecognitionResult  | Response.JobsDetail.Operation | Speech recognition job result. It is not returned when there is no result. | Container |

`SpeechRecognitionResult` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:-------------| :---------------------------- |:------------------------------------------------------------------------------------------| :-------- |
| AudioTime    | Response.JobsDetail.Operation.SpeechRecognitionResult | Audio duration (seconds)                                                                                   | String |
| Result       | Response.JobsDetail.Operation.SpeechRecognitionResult | Speech recognition result                                                                                    | String |
| FlashResult  | Response.JobsDetail.Operation.SpeechRecognitionResult | Result of fast speech recognition                                                                                  | Container array |
| ResultDetail     | Response.JobsDetail.Operation.SpeechRecognitionResult | Recognition result details, including the time offsets of words in each sentence (generally used to generate subtitles). This field will not be empty if `ResTextFormat` in the speech recognition request is `1`.<br/>Note: This field may be empty, indicating that no valid values can be obtained. | Container array |

`FlashResult` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------- | :------------------------------- | :-------- |
| channel_id      | Response.JobsDetail.Operation.SpeechRecognitionResult.FlashResult | Sound channel ID, which starts from 0 and is corresponding to the number of audio channels | Integer |
| text      | Response.JobsDetail.Operation.SpeechRecognitionResult.FlashResult | Complete audio recognition results of the sound channel  | String |
| sentence_list            | Response.JobsDetail.Operation.SpeechRecognitionResult.FlashResult   | List of recognition results at sentence/paragraph level | Container array |

`sentence_list` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- |:-------------------------------------------------------------------| :------------------------------- | :-------- |
| text      | Response.JobsDetail.Operation.SpeechRecognitionResult.FlashResult.sentence_list | Sentence/paragraph-level text | String |
| start_time      | Response.JobsDetail.Operation.SpeechRecognitionResult.FlashResult.sentence_list  | Start time | Integer |
| end_time            | Response.JobsDetail.Operation.SpeechRecognitionResult.FlashResult.sentence_list  | End time | Integer |
| speaker_id            | Response.JobsDetail.Operation.SpeechRecognitionResult.FlashResult.sentence_list  | Speaker ID (If speaker_diarization is set in the request, speakers can be distinguished by `speaker_id`.) | Integer |
| word_list            | Response.JobsDetail.Operation.SpeechRecognitionResult.FlashResult.sentence_list  | List of recognition results at word level | Container array |

`word_list` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- |:---------------------------------------------------------------------------------| :------------------------------- | :-------- |
| word      | Response.JobsDetail.Operation.SpeechRecognitionResult.FlashResult.sentence_list.word_list | Word-level text | String |
| start_time      | Response.JobsDetail.Operation.SpeechRecognitionResult.FlashResult.sentence_list.word_list  | Start time | Integer |
| end_time            | Response.JobsDetail.Operation.SpeechRecognitionResult.FlashResult.sentence_list.word_list | End time | Integer |

`ResultDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------- | :------------------------------- | :-------- |
| FinalSentence      | Response.JobsDetail.Operation.SpeechRecognitionResult.ResultDetail | Final recognition result of a single sentence | String |
| SliceSentence      | Response.JobsDetail.Operation.SpeechRecognitionResult.ResultDetail | Middle recognition result of a single sentence, which is split into multiple words using spaces | String |
| StartMs            | Response.JobsDetail.Operation.SpeechRecognitionResult.ResultDetail   | Start time of a single sentence (millisecond) | String |
| EndMs              | Response.JobsDetail.Operation.SpeechRecognitionResult.ResultDetail   | End time of a single sentence (millisecond) | String |
| WordsNum           | Response.JobsDetail.Operation.SpeechRecognitionResult.ResultDetail   | Number of words in a single sentence | String |
| SpeechSpeed        | Response.JobsDetail.Operation.SpeechRecognitionResult.ResultDetail | Speed of a single sentence. Unit: words/second | String |
| SpeakerId          | Response.JobsDetail.Operation.SpeechRecognitionResult.ResultDetail | Sound channel or speaker ID (If speaker_diarization is set or `ChannelNum` is set to `Dual` in the request, the speakers or channels can be distinguished.) | String |
| Words              | Response.JobsDetail.Operation.SpeechRecognitionResult.ResultDetail | Word details in a single sentence | Container array |

`Words` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------- | :------------------------------- | :-------- |
| Word               | Response.JobsDetail.Operation.SpeechRecognitionResult.ResultDetail.Words | Word text | String |
| OffsetStartMs      | Response.JobsDetail.Operation.SpeechRecognitionResult.ResultDetail.Words | Start time offset in a sentence | String |
| OffsetEndMs        | Response.JobsDetail.Operation.SpeechRecognitionResult.ResultDetail.Words | End time offset in a sentence | String |

#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).

## Examples

#### Request

```shell
POST /asr_jobs HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: test-1234567890.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Tag>SpeechRecognition</Tag>
    <Input>
        <Object>input/test.mp3</Object>
    </Input>
    <Operation>
        <SpeechRecognition>
            <EngineModelType>16k_zh_video</EngineModelType>
            <ChannelNum>1</ChannelNum>
            <FilterDirty>1</ChannelNum>
            <FilterModal>1</ChannelNum>
        </SpeechRecognition>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/asr.txt</Object>
        </Output>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
    <QueueId>pcd463e1467964d39ad2d3f66aacd8199</QueueId>
    <CallBack>http://callback.demo.com</CallBack>
    <CallBackFormat>JSON<CallBackFormat>
</Request>
```

#### Response

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
        <CreationTime>2021-08-05T15:43:50+0800</CreationTime>
        <EndTime>-</EndTime>
        <Input>
            <BucketId>test-1234567890</BucketId>
            <Object>input/test.mp3</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>s58ccb634149211ed84ce2b1cd7fbb14a</JobId>
        <Message/>
        <Operation>
            <JobLevel>0</JobLevel>
            <Output>
                <Bucket>test-1234567890</Bucket>
                <Object>output/asr.txt</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <SpeechRecognition>
                <ChannelNum>1</ChannelNum>
                <ConvertNumMode>0</ConvertNumMode>
                <EngineModelType>16k_zh_video</EngineModelType>
                <FilterDirty>0</FilterDirty>
                <FilterModal>0</FilterModal>
                <FilterPunc>0</FilterPunc>
                <OutputFileType>txt</OutputFileType>
                <ResTextFormat>0</ResTextFormat>
                <SpeakerDiarization>0</SpeakerDiarization>
                <SpeakerNumber>0</SpeakerNumber>
            </SpeechRecognition>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
        <QueueId>pcd463e1467964d39ad2d3f66aacd8199</QueueId>
        <StartTime>-</StartTime>
        <State>Submitted</State>
        <Tag>SpeechRecognition</Tag>
    </JobsDetail>
</Response>
```
