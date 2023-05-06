## Feature Overview

This API is used to submit a splicing job.



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
>
> Authorization: Auth String. For more information, see [Request Signature](https://www.tencentcloud.com/document/product/436/7778).
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://www.tencentcloud.com/document/product/1045/49896).

#### Request headers

This API only uses [Common Request Headers](https://www.tencentcloud.com/document/product/1045/43609).

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
            <Object>output/out.${ext}</Object>
        </Output>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
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
| ------------------ | ------- | ------------------------------------------------------------ | --------- | -------- |
| Tag                | Request | Job type: `Concat`                                   | String    | Yes   |
| Input              | Request | Information about the file to be operated                                         | Container | No   |
| Operation          | Request | Operation rule                                  | Container | Yes   |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default value). It takes priority over that of the queue. | String | No |
| CallBackType       | Request | Job callback type, which can be `Url` (default value) or `TDMQ`. It takes priority over that of the queue.                    | String | No |
| CallBack           | Request | Job callback address, which takes priority over that of the queue. If it is set to `no`, no callbacks will be generated at the callback address of the queue. | String | No |
| CallBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure](https://www.tencentcloud.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |


`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | -------- | ------ | -------- |
| Object             | Request.Input | File path | String | Yes       |

<span id="operation"></span>
`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | -------- |
| ConcatTemplate     | Request.Operation | Splicing parameter                                                 | Container | No       |
| TemplateId                   | Request.Operation | Template ID                                        | String    | No  |
| Output                       | Request.Operation | Result output configuration                                        | Container | Yes   |
| JobLevel            | Request.Operation | Job priority. The greater the value, the higher the priority. Valid values: `0` (default), `1`, `2`. | String | No |


>!`TemplateId` is used first. If `TemplateId` is unavailable, `ConcatTemplate` is used.

`ConcatTemplate` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | -------------------------------- | ------------------------------------------------------------ | -------------- | -------- | ------ | --------------------------------- |
| ConcatFragment     | Request.Operation. ConcatTemplate | Splicing node                                                    | Container array | No       | None     | Multiple files can be spliced in sequence. |
| Audio               |  Request.Operation.ConcatTemplate | Audio parameter. Same as <a href="https://cloud.tencent.com/document/product/460/84730#Audio" target="_blank">Request.ConcatTemplate.Audio</a> in the splicing template creation API  | Container    | No   | None  | None |
| Video               |  Request.Operation.ConcatTemplate | Video parameter. Same as <a href="https://cloud.tencent.com/document/product/460/84730#Video" target="_blank">Request.ConcatTemplate.Video</a> in the splicing template creation API  | Container    | No   | None  | None |
| Container           |  Request.Operation.ConcatTemplate | Container format. Same as <a href="https://cloud.tencent.com/document/product/460/84730#Container" target="_blank">Request.ConcatTemplate.Container</a> in the splicing template creation API   | Container    | Yes   | None  | None |
| AudioMix           | Request.Operation.ConcatTemplate | Audio mix parameter as described in <a href="https://intl.cloud.tencent.com/document/product/1045/49945" target="_blank">AudioMix</a>                                    | Container array | No   | None | Valid only if `Audio.Remove` is `false` |
| AudioMixArray      | Request.Operation.Transcode      | Audio mix parameter array as described in <a href="https://intl.cloud.tencent.com/document/product/1045/49945Array" target="_blank">AudioMixArray</a>. A maximum of two parameters can be passed in. | Container array  | No       |    None    |           None                        |
| Index              | Request.Operation.ConcatTemplate | Index of the `Input` node in the `ConcatFragment` sequence    | String    | No   | 0  | The number of indexes configured cannot be greater than the number of fragments specified by `ConcatFragment`. |
| DirectConcat       | Request.Operation.ConcatTemplate | Simple splicing (without transcoding). Other video and audio parameters become invalid. | String | No | false | true, false |

>? If both `AudioMix` and `AudioMixArray` are specified, `AudioMixArray` is invalid.

`ConcatFragment` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | --------------------------------------------------------- | ------------------ | ------ | -------- | -------- | ---------------------------------------- |
| Url                 | Request.Operation.<br/>ConcatTemplate.<br/>ConcatFragment | Concatenation object address   | String    | Yes   | None   | Same as the address of the bucket object file. |
| FragmentIndex       | Request.Operation.<br/>ConcatTemplate.<br/>ConcatFragment | Index position of the spliced object    | String    | No   | 0   | An integer greater than or equal to 0 |
| StartTime           | Request.Operation.<br/>ConcatTemplate.<br/>ConcatFragment | Start time   | String    | No   | Video start time   | <li>[0, Video duration] </li><li>Unit: second </li>  |
| EndTime           | Request.Operation.<br/>ConcatTemplate.<br/>ConcatFragment | End time   | String    | No   | Video end time   | <li>[0, Video duration] </li><li>Unit: second </li>  |



`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------ | ---------------- | ------ | -------- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Output result filename                                             | String | Yes   |

`Request.Operation.Output.Object` supports the following wildcards:

| Wildcard   | Meaning     |
| -------- | -------- |
| ${ext}   | Container format |
| ${jobid}           | Job ID |


## Response

#### Response headers

This API only returns [Common Response Headers](https://www.tencentcloud.com/document/product/1045/43610).

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
                <Object>output/out.${ext}</Object>
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
| Tag                | Response.JobsDetail | Job type: `Concat`                              | String    |
| State | Response.JobsDetail | Job status. Valid values: Submitted, Running, Success, <br/>Failed, Pause, Cancel. |  String |
| CreationTime       | Response.JobsDetail | Task creation time                         | String    |
| StartTime          | Response.JobsDetail | Job start time                                               | String    |
| EndTime          | Response.JobsDetail | Job end time                                               | String    |
| QueueId            | Response.JobsDetail | ID of the queue where the job is in                                             | String    |
| Input              | Response.JobsDetail | Input resource address of the job                   | Container |
| Operation          | Response.JobsDetail | Operation rule                           | Container |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------------- | ---------------- | ------ |
| Region             | Response.JobsDetail.Input | Bucket region                                | String    |
| Bucket          | Response.JobsDetail.Input | Result storage bucket                                 | String    |
| Object             | Response.JobsDetail.Input | Output result filename | String |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------- | :------------------------------------------ | :-------- |
| TemplateId         | Response.JobsDetail.Operation | Job template ID                     | String    |
| TemplateName         | Response.JobsDetail.Operation | Job template name, which is returned when `TemplateId` exists    | String    |
| ConcatTemplate             | Response.JobsDetail.Operation | Same as `Request.Operation.ConcatTemplate` in the request  | Container |
| Output | Response.JobsDetail.Operation | Same as `Request.Operation.Output` in the request |  Container |
| MediaInfo | Response.JobsDetail.Operation | Media information of the output file, which will not be returned when the job is not completed |  Container |
| MediaResult        | Response.JobsDetail.Operation | Basic information of the output file, which will not be returned when the job is not completed | Container |
| UserData           | Response.JobsDetail.Operation | The user information passed through                      | String |
| JobLevel    | Response.JobsDetail.Operation | Job priority                                                         | String |

`MediaInfo` has the following sub-nodes:
Same as the `Response.MediaInfo` node in the [Getting Media File Information](https://www.tencentcloud.com/document/product/1045/43732) API.

`MediaResult` has the following sub-nodes:
For more information, see <a href="https://intl.cloud.tencent.com/document/product/1045/49945" target="_blank">MediaResult</a>.

#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://www.tencentcloud.com/document/product/1045/33700).

## Examples

#### Request 1: Using a transcoding template ID

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
            <Object>output/out.${ext}</Object>
        </Output>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
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
x-ci-request-id: NjMxMDJhYTNfMThhYTk0MGFfYmU1OV8zZjc=

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
                <Object>output/out.${ext}</Object>
            </Output>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```


#### Request 2: Using the splicing parameter

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
            <AudioMixArray>
                <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix1.mp3</AudioSource>
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
            </AudioMixArray>
            <AudioMixArray>
                <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix2.mp3</AudioSource>
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
            </AudioMixArray>
        </ConcatTemplate>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/out.${ext}</Object>
        </Output>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
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
x-ci-request-id: NjMxMDJhYTNfMThhYTk0MGFfYmU1OV8zZjc=

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
                <AudioMixArray>
                    <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix1.mp3</AudioSource>
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
                </AudioMixArray>
                <AudioMixArray>
                    <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix2.mp3</AudioSource>
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
                </AudioMixArray>
                <Index>1</Index>
            </ConcatTemplate>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>output/out.${ext}</Object>
            </Output>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```

#### Request 3: Splicing multiple files

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
            <Object>output/out.${ext}</Object>
        </Output>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
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
x-ci-request-id: NjMxMDJhYTNfMThhYTk0MGFfYmU1OV8zZjc=

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
                <Object>output/out.${ext}</Object>
            </Output>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```
