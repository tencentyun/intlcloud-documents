## Feature Description

This API (`CreateSpeechJobs`) is used to submit a speech recognition job.

## Request

#### Sample request

```plaintext
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
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see Authorization Granularity.
> 

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```plaintext
<Request>
  <Tag>SpeechRecognition</Tag>
  <Input>
    <Object></Object>
  </Input>
  <Operation>
    <SpeechRecognition></SpeechRecognition>
    <Output>
      <Region></Region>
      <Bucket></Bucket>
      <Object></Object>
    </Output>
  </Operation>
  <QueueId></QueueId>
</Request>
```

The nodes are as described below:

<table>
   <tr>
      <th nowrap="nowrap">Node Name (Keyword)</th>
      <th>Parent Node</th>
      <th>Description</th>
      <th>Type</th>
      <th>Required</th>
   </tr>
   <tr>
      <td>Request</td>
      <td>None</td>
      <td>Request container</td>
      <td>Container</td>
      <td>Yes</td>
   </tr>
</table>

`Request` has the following sub-nodes:

<table>
   <tr>
      <th nowrap="nowrap">Node Name (Keyword)</th>
      <th>Parent Node</th>
      <th>Description</th>
      <th>Type</th>
      <th>Required</th>
   </tr>
   <tr>
      <td>Tag</td>
      <td>Request</td>
      <td>Job type, which currently can only be `SpeechRecognition`.</td>
      <td>String</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Input</td>
      <td>Request</td>
      <td>Speech file to be manipulated</td>
      <td>Container</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Operation</td>
      <td>Request</td>
      <td>Operation rule</td>
      <td>Container</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>QueueId</td>
      <td>Request</td>
      <td>ID of the queue which the job is in</td>
      <td>String</td>
      <td>Yes</td>
   </tr>
</table>

`Input` has the following sub-nodes:

<table>
   <tr>
      <th nowrap="nowrap">Node Name (Keyword)</th>
      <th>Parent Node</th>
      <th>Description</th>
      <th>Type</th>
      <th>Required</th>
   </tr>
   <tr>
      <td>Object</td>
      <td>Request.Input</td>
      <td>Speech file key in COS. `Bucket` is specified by `Host`.</td>
      <td>String</td>
      <td>Yes</td>
   </tr>
</table>

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | -------- |
| SpeechRecognition  | Request.Operation | Job type parameter, which takes effect only if `Tag` is `SpeechRecognition`.          | Container | No      |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |


`SpeechRecognition` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | :-------------------------- | ----------------------------------------- | --------- | -------- |
| EngineModelType    | Request.Operation.Speech<br>Recognition | Engine model type. <br>Phone call scenarios: <br>• 8k_zh: 8 kHz, for Mandarin in general scenarios (available for dual-channel audio). <br> • 8k_zh_s: 8 kHz, for Mandarin with speaker separation (available for mono-channel audio only). <br> Non-phone call scenarios: <br> • 16k_zh: 16 kHz, for Mandarin in general scenarios. <br> • 16k_zh_video: 16 kHz, for Mandarin in audio/video scenarios. <br> • 16k_en: 16 kHz, for English. <br> • 16k_ca: 16 kHz, for Cantonese. | String | Yes |
| ChannelNum         | Request.Operation.Speech<br>Recognition | Number of speech sound channels. 1: mono; 2: dual (for the 8k_zh engine only). | Integer | Yes |
| ResTextFormat       | Request.Operation.Speech<br>Recognition | Format of the returned recognition result. 0: recognition result text, including the list of segment timestamps; 1: recognition result details, including the list of word timestamps (generally used to generate subtitles and for the 16k Mandarin engine only). | Integer | Yes |
| FilterDirty       | Request.Operation.Speech<br>Recognition | Whether to filter restricted words (for the Mandarin engine only). 0 (default value): does not filter; 1: filters; 2: replaces restricted words with "*". | Integer | No       |
| FilterModal       | Request.Operation.Speech<br>Recognition | Whether to filter interjections (for the Mandarin engine only). 0 (default value): does not filter; 1: filters; 2: filters strictly. | Integer | No       |
| ConvertNumMode       | Request.Operation.Speech<br>Recognition | Whether to intelligently convert Chinese numbers to Arabic numerals (for the Mandarin engine only). 0: directly outputs Chinese numbers; 1 (default value): intelligently converts based on the scenario. | Integer | No       |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------ | ------------------------------------------------------------ | ------ | -------- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Result filename                                             | String | Yes   |



## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
  <JobsDetail>
    <Code></Code>
    <Message></Message>
    <JobId></JobId>
    <State></State>
    <CreationTime></CreationTime>
    <QueueId></QueueId>
    <Tag><Tag>
    <Input>
      <Object></Object>
    </Input>
    <Operation>
      <SpeechRecognition></SpeechRecognition>
      <Output>
        <Region></Region>
        <Bucket></Bucket>
        <Object></Object>
      </Output>
      <MediaInfo>
      </MeidaInfo>
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

`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :-------- |
| Code               | Response.JobsDetail | Error code, which is meaningful only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error description, which is meaningful only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Job ID                               | String    |
| Tag | Response.JobsDetail | Job type: SpeechRecognition | String |
| State | Response.JobsDetail | Job status. Valid values: Submitted, Running, Success, Failed, Pause, Cancel |  String |
| CreationTime       | Response.JobsDetail | Job creation time                         | String    |
| QueueId            | Response.JobsDetail | ID of the queue which the job is in                       | String    |
| Input              | Response.JobsDetail | Input resource address of the job                   | Container |
| Operation          | Response.JobsDetail | Operation rule                           | Container |

`Input` has the following sub-nodes:
Same as the `Request.Input` node in the request.

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------- | :------------------------------- | :-------- |
| TemplateId | Response.JobsDetail.Operation | Job template ID |  String |
| Output             | Response.JobsDetail.Operation | File output address   | Container |
| MediaInfo          | Response.JobsDetail.Operation | Transcoding output video information. This node will not be returned if there is no output video. | Container |

`Output` has the following sub-nodes:
Same as the `Request.Operation.Output` node in the request.

`SpeechRecognition` has the following sub-nodes:
Same as the `Request.Operation.SpeechRecognition` node in the request.

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

