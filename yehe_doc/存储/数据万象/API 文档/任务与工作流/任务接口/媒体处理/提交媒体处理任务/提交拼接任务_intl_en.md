## Feature Description

This API (`CreateMediaJobs`) is used to submit a job.

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
> - When this feature is used by a sub-account, relevant permissions must be granted.
> 


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body
This request requires the following request body:

```shell
<Request>
  <Tag>Concat</Tag>
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

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Tag                | Request | Job type: Concat                                   | String    | Yes   |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule. Up to six jobs can be performed on the same file.                                                | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |
| CallBack           | Request | Callback address                                                | String    | No   |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | --------------- | ------ | ---- |
| Object             | Request.Input | Media filename | String | Yes   |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | ---- |
| ConcatTemplate               | Request.Operation | Same as `Request.ConcatTemplate` in the splicing template creation API `CreateMediaTemplate`.    | Container | No   |
| TemplateId                   | Request.Operation | Template ID                                        | String    | No  |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |

>! If `ConcatTemplate` and `TemplateId` exist at the same time, the transcoding parameter in `TemplateId` will be used first.
>

`ConcatTemplate` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------  | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| ConcatFragment      |  Request.Operation.<br/>ConcatTemplate | Splicing node                                                    | Container array | No       | None     | Multiple files can be spliced in sequence. |
| Audio               |  Request.Operation.<br/>ConcatTemplate | Audio parameter. Same as `Request.ConcatTemplate.Audio` in the splicing template creation API.  | Container    | No   | None  | None |
| Video               |  Request.Operation.<br/>ConcatTemplate | Video parameter. Same as `Request.ConcatTemplate.Video` in the splicing template creation API.  | Container    | No   | None  | None |
| Container           |  Request.Operation.<br/>ConcatTemplate | Container format. Same as `Request.ConcatTemplate.Container` in the splicing template creation API.   | Container    | Yes   | None  | None |
| Index               |  Request.Operation.<br/>ConcatTemplate| Index of the `Input` node in the `ConcatFragment` sequence    | String    | No   | 0  | The number of indexes configured cannot be greater than the number of fragments specified by `ConcatFragment`. |
| DirectConcat | Request.Operation.<br/>ConcatTemplate | Simple splicing (without transcoding). Other video and audio parameters become invalid. | String | No | false | true, false |

`ConcatFragment` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------  | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Url                 | Request.Operation.<br/>ConcatTemplate.<br/>ConcatFragment | Splicing object address   | String    | Yes   | None   | Same as the address of the bucket object file. |
| FragmentIndex       | Request.Operation.<br/>ConcatTemplate.<br/>ConcatFragment | Index position of the spliced object    | String    | No   | 0   | An integer greater than or equal to 0 |
| StartTime           | Request.Operation.<br/>ConcatTemplate.<br/>ConcatFragment | Start time   | String    | No   | Video start time   | <li>[0, video duration] </li><li>Unit: second </li>  |
| EndTime             | Request.Operation.<br/>ConcatTemplate.<br/>ConcatFragment | End time   | String    | No   | Video end time   | <li>[0, video duration] </li><li>Unit: second </li>  |



`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------ | ------------------------------------------------------------ | ------ | ---- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Output result filename                                             | String | Yes   |



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
    <Tag>Concat</Tag>
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
      <MediaInfo>
      </MeidaInfo>
    </Operation>
  </JobsDetail>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Response | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| JobsDetail | Response | Job details |  Container |


`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Code               | Response.JobsDetail | Error code, which is returned only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error message, which is returned only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Job ID                               | String    |
| Tag                | Response.JobsDetail | Job type: Concat                              | String    |
| State | Response.JobsDetail | Job status. Valid values: Submitted, Running, Success, <br/>Failed, Pause, Cancel. |  String |
| CreationTime | Response.JobsDetail | Job creation time |  String |
| StartTime | Response.JobsDetail | Job start time |  String |
| EndTime | Response.JobsDetail | Job end time |  String |
| QueueId            | Response.JobsDetail | Queue ID of the job                       | String    |
| Input              | Response.JobsDetail | Input resource address of the job                   | Container |
| Operation | Response.JobsDetail | Operation rule. Up to six jobs can be performed on the same file. |  Container |

`Input` has the following sub-nodes:
Same as the `Request.Input` node in the request.

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| TemplateId | Response.JobsDetail.Operation | Job template ID |  String |
| Output             | Response.JobsDetail.Operation | File output address               | Container |
| MediaInfo          | Response.JobsDetail.Operation | Transcoding output video information. This node will not be returned when there is no output video. | Container |

`Output` has the following sub-nodes:
Same as the `Request.Operation.Output` node in the request.

`MediaInfo` has the following sub-nodes:
Same as the `Response.MediaInfo` node in the `GenerateMediaInfo` API.


#### Error codes
For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

**Using the splicing template ID**

#### Request

```shell
POST /jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98****-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml



<Request>
  <Tag>Concat</Tag>
  <Input>
    <Object>test.mp4</Object>
  </Input>
  <Operation>
    <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
    <Output>
      <Region>ap-beijing</Region>
      <Bucket>aabc-1250000000</Bucket>
      <Object>concat.mp4</Object>
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
    <JobId>je8f65004eb8511eaaed4f377124a303c</JobId>
    <State>Submitted</State>
    <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    <EndTime></EndTime>
    <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
    <Tag>Concat</Tag>
    <Input>
      <Object>test.mp4</Object>
    </Input>
    <Operation>
      <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
      <Output>
        <Region>ap-beijing</Region>
        <Bucket>aabc-1250000000</Bucket>
        <Object>concat.mp4</Object>
      </Output>
    </Operation>
  </JobsDetail>
</Response>
```


**Using the splicing processing parameter**

#### Request

```shell
POST /jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98****-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml



<Request>
  <Tag>Concat</Tag>
  <Input>
    <Object>test.mp4</Object>
  </Input>
  <Operation>
    <ConcatTemplate>
        <ConcatFragment>
            <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/start.mp4</Url>
        </ConcatFragment>
        <ConcatFragment>
            <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/end.mp4</Url>
        </ConcatFragment>
        <Audio>
            <Codec>mp3</Codec>
            <Samplerate></Samplerate>
            <Bitrate></Bitrate>
            <Channels></Channels>
        </Audio>
        <Video>
            <Codec>H.264</Codec>
            <Bitrate>1000</Bitrate>
            <Width>1280</Width>
            <Height></Height>
            <Fps>30</Fps>
        </Video>
        <Container>
            <Format>mp4</Format>
        </Container>
        <AudioMix>
            <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix.mp3</AudioSource>
            <MixMode>Once</MixMode>
            <Replace>true</Replace>
            <EffectConfig>
                <EnableStartFadein>true</EnableStartFadein>
                <StartFadeinTime>3</StartFadeinTime>
                <EnableEndFadeout>false</EnableEndFadeout>
                <EndFadeoutTime>0</EndFadeoutTime>
                <EnableBgmFade>true</EnableBgmFade>
                <BgmFadeTime>1.7</BgmFadeTime>
            </EffectConfig>
        </AudioMix>
    </ConcatTemplate>
    <Output>
      <Region>ap-beijing</Region>
      <Bucket>aabc-1250000000</Bucket>
      <Object>concat.mp4</Object>
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
    <Tag>Concat</Tag>
    <Input>
      <Object>test.mp4</Object>
    </Input>
    <Operation>
        <ConcatTemplate>
            <ConcatFragment>
                <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/start.mp4</Url>
            </ConcatFragment>
            <ConcatFragment>
                <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/end.mp4</Url>
            </ConcatFragment>
            <Audio>
                <Codec>mp3</Codec>
                <Samplerate></Samplerate>
                <Bitrate></Bitrate>
                <Channels></Channels>
            </Audio>
            <Video>
                <Codec>H.264</Codec>
                <Bitrate>1000</Bitrate>
                <Width>1280</Width>
                <Height></Height>
                <Fps>30</Fps>
            </Video>
            <Container>
                <Format>mp4</Format>
            </Container>
            <AudioMix>
              <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix.mp3</AudioSource>
              <MixMode>Once</MixMode>
              <Replace>true</Replace>
              <EffectConfig>
                  <EnableStartFadein>true</EnableStartFadein>
                  <StartFadeinTime>3</StartFadeinTime>
                  <EnableEndFadeout>false</EnableEndFadeout>
                  <EndFadeoutTime>0</EndFadeoutTime>
                  <EnableBgmFade>true</EnableBgmFade>
                  <BgmFadeTime>1.7</BgmFadeTime>
              </EffectConfig>
            </AudioMix>
        </ConcatTemplate>
        <Output>
            <Region>ap-beijing</Region>
            <Bucket>aabc-1250000000</Bucket>
            <Object>concat.mp4</Object>
        </Output>
    </Operation>
  </JobsDetail>
</Response>
```
