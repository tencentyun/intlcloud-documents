## Feature Description

This API is used to submit a splicing job.

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
    <Tag>Concat</Tag>
    <Input>
        <Object>input/demo.mp4</Object>
    </Input>
    <Operation>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
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
| ------------------ | ------- | ------------------------------------------------------- | --------- | -------- |
| Tag                | Request | Job tag: Concat                                   | String    | Yes   |
| Input              | Request | Information of the media file to be processed                                         | Container | No   |
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
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | -------- |
| ConcatTemplate     | Request.Operation | Splicing parameter.                                                 | Container | No       |
| TemplateId                   | Request.Operation | Template ID                                        | String    | No  |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |
| JobLevel            | Request.Operation | Job priority. The greater the value, the higher the priority. Valid values: `0`, `1`, `2`. Default value: `0`. | String | No |


>! `TemplateId` is used first. If `TemplateId` is unavailable, `ConcatTemplate` is used.

`ConcatTemplate` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------------------------------- | ------------------------------------------------------------ | -------------- | -------- | ------ | ------------------------------ |
| ConcatFragment      |  Request.Operation.<br/>ConcatTemplate | Splicing node                                                    | Container array | No       | None     | Multiple files can be spliced in sequence. |
| Audio               |  Request.Operation.<br/>ConcatTemplate | Audio parameter. Same as `Request.ConcatTemplate.Audio` in the splicing template creation API <a href="https://intl.cloud.tencent.com/document/product/1045/49907" target="_blank">CreateMediaTemplate</a>.  | Container    | No   | None  | None |
| Video               |  Request.Operation.<br/>ConcatTemplate | Video parameter. Same as `Request.ConcatTemplate.Video` in the splicing template creation API <a href="https://intl.cloud.tencent.com/document/product/1045/49907" target="_blank">CreateMediaTemplate</a>.  | Container    | No   | None  | None |
| Container           |  Request.Operation.<br/>ConcatTemplate | Container format. Same as `Request.ConcatTemplate.Container` in the splicing template creation API <a href="https://intl.cloud.tencent.com/document/product/1045/49907" target="_blank">CreateMediaTemplate</a>.   | Container    | Yes   | None  | None |
| AudioMix           | Request.Operation.<br/>ConcatTemplate | Audio mix parameter as described in <a href="https://intl.cloud.tencent.com/document/product/1045/49945" target="_blank">Structure</a>.                                    | Container array | No   | None | Valid only if `Audio.Remove` is `false` |
| Index              | Request.Operation.<br/>ConcatTemplate | Index of the `Input` node in the `ConcatFragment` sequence    | String    | No   | 0  | The number of indexes configured cannot be greater than the number of fragments specified by `ConcatFragment`. |
| DirectConcat | Request.Operation.<br/>ConcatTemplate | Simple splicing (without transcoding). Other video and audio parameters become invalid. | String | No | false | true, false |

`ConcatFragment` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | --------------------------------------------------------- | ------------------ | ------ | -------- | -------- | ---------------------------------------- |
| Url                 | Request.Operation.<br/>ConcatTemplate.<br/>ConcatFragment | Splicing object address   | String    | Yes   | None   | Same as the address of the bucket object file. |
| FragmentIndex       | Request.Operation.<br/>ConcatTemplate.<br/>ConcatFragment | Index position of the spliced object    | String    | No   | 0   | An integer greater than or equal to 0 |
| StartTime           | Request.Operation.<br/>ConcatTemplate.<br/>ConcatFragment | Start time   | String    | No   | Video start time   | <li>[0, video duration] </li><li>Unit: Second </li>  |
| EndTime             | Request.Operation.<br/>ConcatTemplate.<br/>ConcatFragment | End time   | String    | No   | Video end time   | <li>[0, video duration] </li><li>Unit: Second </li>  |



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
        <CreationTime>2022-06-27T15:23:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Tag>Concat</Tag>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
            <TemplateName>concat_demo</TemplateName>
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
| Tag                | Response.JobsDetail | Job tag: Concat                              | String    |
| State | Response.JobsDetail | Job status. Valid values: `Submitted`, `Running`, `Success`, <br/>`Failed`, `Pause`, `Cancel`. |  String |
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
| :----------------- | :---------------------------- | :------------------------------- | :-------- |
| TemplateId | Response.JobsDetail.Operation | Job template ID |  String |
| TemplateName        | Response.JobsDetail.Operation | Job template name, which will be returned if `TemplateId` exists. | String    |
| ConcatTemplate             | Response.JobsDetail.Operation | Same as `Request.Operation.ConcatTemplate` in the request.  | Container |
| Output             | Response.JobsDetail.Operation | Same as `Request.Operation.Output` in the request.  | Container |
| MediaInfo           | Response.JobsDetail.Operation | Media information of the output file, which will not be returned when the job is not completed. | Container |
| MediaResult        | Response.JobsDetail.Operation | Basic information of the output file, which will not be returned when the job is not completed. | Container |
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



#### Error codes

For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).

## Samples

#### Request 1. Using the splicing template ID

#### Request

```shell
POST /jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98****-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host:test-123456789.ci.ap-chongqing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Tag>Concat</Tag>
    <Input>
        <Object>input/demo.mp4</Object>
    </Input>
    <Operation>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
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

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Mon, 28 Jun 2022 15:23:12 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzh****=

<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>j8d121820f5e411ec926ef19d53ba9c6f</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T15:23:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Tag>Concat</Tag>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
            <TemplateName>concat_demo</TemplateName>
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


#### Request 2. Using the splicing parameter

#### Request

```shell
POST /jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98****-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host:test-123456789.ci.ap-chongqing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Tag>Concat</Tag>
    <Input>
        <Object>input/demo.mp4</Object>
    </Input>
    <Operation>
        <ConcatTemplate>
            <ConcatFragment>
                <Url>http://test-123456789.cos.ap-chongqing.myqcloud.com/start.mp4</Url>
            </ConcatFragment>
            <ConcatFragment>
                <Url>http://test-123456789.cos.ap-chongqing.myqcloud.com/end.mp4</Url>
            </ConcatFragment>
            <Audio>
                <Codec>mp3</Codec>
            </Audio>
            <Video>
                <Codec>H.264</Codec>
                <Bitrate>1000</Bitrate>
                <Width>1280</Width>
                <Height>720</Height>
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

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Mon, 28 Jun 2022 15:23:12 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzh****=

<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>j8d121820f5e411ec926ef19d53ba9c5d</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T15:23:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Tag>Concat</Tag>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <ConcatTemplate>
                <ConcatFragment>
                    <Url>http://test-123456789.cos.ap-chongqing.myqcloud.com/start.mp4</Url>
                </ConcatFragment>
                <ConcatFragment>
                    <Url>http://test-123456789.cos.ap-chongqing.myqcloud.com/end.mp4</Url>
                </ConcatFragment>
                <Audio>
                    <Codec>mp3</Codec>
                </Audio>
                <Video>
                    <Codec>H.264</Codec>
                    <Bitrate>1000</Bitrate>
                    <Width>1280</Width>
                    <Height>720</Height>
                    <Fps>30</Fps>
                </Video>
                <Container>
                    <Format>mp4</Format>
                </Container>
                <AudioMix>
                    <AudioSource>https://test-123456789.cos.ap-chongqing.myqcloud.com/mix.mp3</AudioSource>
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
                <Index>1</Index>
            </ConcatTemplate>
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

#### Request 3. Splicing multiple files

#### Request

```shell
POST /jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98****-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host:test-123456789.ci.ap-chongqing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Tag>Concat</Tag>
    <Operation>
        <ConcatTemplate>
            <ConcatFragment>
                <Url>http://test-123456789.cos.ap-chongqing.myqcloud.com/start.mp4</Url>
                <FragmentIndex>0</FragmentIndex>
                <StartTime>0</StartTime>
                <EndTime>6</EndTime>
            </ConcatFragment>
            <ConcatFragment>
                <Url>http://test-123456789.cos.ap-chongqing.myqcloud.com/middle.mp4</Url>
                <FragmentIndex>1</FragmentIndex>
            </ConcatFragment>
            <ConcatFragment>
                <Url>http://test-123456789.cos.ap-chongqing.myqcloud.com/end.mp4</Url>
                <FragmentIndex>2</FragmentIndex>
                <StartTime>5</StartTime>
                <EndTime>10</EndTime>
            </ConcatFragment>
            <Container>
                <Format>mp4</Format>
            </Container>
        </ConcatTemplate>
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

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Mon, 28 Jun 2022 15:23:12 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzh****=

<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>j8d121820f5e411ec926ef19d53ba9c5d</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T15:23:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Tag>Concat</Tag>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <ConcatTemplate>
                <ConcatFragment>
                    <Url>http://test-123456789.cos.ap-chongqing.myqcloud.com/start.mp4</Url>
                    <StartTime>0</StartTime>
                    <EndTime>6</EndTime>
                </ConcatFragment>
                <ConcatFragment>
                    <Url>http://test-123456789.cos.ap-chongqing.myqcloud.com/middle.mp4</Url>
                </ConcatFragment>
                <ConcatFragment>
                    <Url>http://test-123456789.cos.ap-chongqing.myqcloud.com/end.mp4</Url>
                    <StartTime>5</StartTime>
                    <EndTime>10</EndTime>
                </ConcatFragment>
                <Container>
                    <Format>mp4</Format>
                </Container>
            </ConcatTemplate>
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
