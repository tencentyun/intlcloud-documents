## Feature Description

This API is used to submit multiple jobs.

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
    <Input>
        <Object>input/demo.mp4</Object>
    </Input>
    <Operation>
        <Tag>Animation</Tag>
        <TemplateId>t1f16e1dfbdc994105b31292d45710642a</TemplateId>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/animation.gif</Object>
        </Output>
        <UserData>This is my Animation job.</UserData>
    </Operation>
    <Operation>
        <Tag>Transcode</Tag>
        <TemplateId>t1995d523e42df4c5e858f244b4174360c</TemplateId>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/transcode.mp4</Object>
        </Output>
        <UserData>This is my Trancode job.</UserData>
    </Operation>
    <Operation>
        <Tag>SmartCover</Tag>
        <SmartCover>
            <Format>jpg</Format>
            <Width>1280</Width>
            <Height>960</Height>
            <Count>5</Count>
            <DeleteDuplicates>true</DeleteDuplicates>
        </SmartCover>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/smartcover-${Number}.jpg</Object>
        </Output>   
        <UserData>This is my SmartCover job.</UserData>
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
| ------------------ | ------- | ----------------------- | --------- | -------- |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule. Up to six operation rules are supported.                                  | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | ---------- | ------ | -------- |
| Object             | Request.Input | Media filename | String | Yes   |

The content of `Operation` varies by job type. For more information, see the following documents:
- <a href="https://intl.cloud.tencent.com/document/product/1045/48941" target="_blank">Submitting Video Transcoding Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/49569" target="_blank">Submitting Video-to-Animated Image Conversion Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48938#operation" target="_blank">Submitting Screenshot Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48937" target="_blank">Submitting Intelligent Thumbnail Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48929" target="_blank">Submitting Video Splicing Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48946" target="_blank">Submitting Voice/Sound Separation Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48943" target="_blank">Submitting Video Montage Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48935" target="_blank">Submitting SDR-to-HDR Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48944" target="_blank">Submitting Video Enhancement Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48940" target="_blank">Submitting Super Resolution Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48936" target="_blank">Submitting Remuxing Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48930" target="_blank">Submitting Digital Watermark Adding Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48931" target="_blank">Submitting Digital Watermark Extracting Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48945" target="_blank">Submitting Video Tagging Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48932" target="_blank">Submitting Media Information Query Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48939" target="_blank">Submitting Stream Separation Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48934" target="_blank">Submitting Video Quality Scoring Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48942" target="_blank">Submitting Text-to-Speech Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48933" target="_blank">Submitting Audio Noise Cancellation Job</a>


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
        <JobId>j682b9662f84611ecb8546d80f2baf56f</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T15:23:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <Tag>Animation</Tag>
            <TemplateId>t1f16e1dfbdc994105b31292d45710642a</TemplateId>
            <TemplateName>animation_demo</TemplateName>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>output/animation.gif</Object>
            </Output>
            <UserData>This is my Animation job.</UserData>
        </Operation>
    </JobsDetail>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>j68427030f84611ecb8546d80f2baf56f</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T15:23:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <Tag>Transcode</Tag>
            <TemplateId>t1995d523e42df4c5e858f244b4174360c</TemplateId>
            <TemplateName>transcode_demo</TemplateName>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>output/transcode.mp4</Object>
            </Output>
            <UserData>This is my Trancode job.</UserData>
        </Operation>
    </JobsDetail>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>j6842765cf84611ecb8546d80f2baf56f</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T15:23:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <Tag>SmartCover</Tag>
            <SmartCover>
                <Format>jpg</Format>
                <Width>1280</Width>
                <Height>960</Height>
                <Count>5</Count>
                <DeleteDuplicates>true</DeleteDuplicates>
            </SmartCover>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>output/smartcover-${Number}.jpg</Object>
            </Output>   
            <UserData>This is my SmartCover job.</UserData>
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
| JobsDetail | Response | Job details |  Container array |

The content of `JobsDetail` varies by job type. For more information, see the following documents:
- <a href="https://intl.cloud.tencent.com/document/product/1045/48941" target="_blank">Submitting Video Transcoding Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/49569" target="_blank">Submitting Video-to-Animated Image Conversion Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48938" target="_blank">Submitting Video Frame Capturing Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48937" target="_blank">Submitting Intelligent Thumbnail Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48929" target="_blank">Submitting Video Splicing Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48946" target="_blank">Submitting Voice/Sound Separation Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48943" target="_blank">Submitting Video Montage Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48935" target="_blank">Submitting SDR-to-HDR Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48944" target="_blank">Submitting Video Enhancement Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48940" target="_blank">Submitting Super Resolution Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48936" target="_blank">Submitting Remuxing Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48930" target="_blank">Submitting Digital Watermark Adding Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48931" target="_blank">Submitting Digital Watermark Extracting Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48945" target="_blank">Submitting Video Tagging Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48932" target="_blank">Submitting Media Information Query Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48939" target="_blank">Submitting Stream Separation Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48934" target="_blank">Submitting Video Quality Scoring Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48942" target="_blank">Submitting Text-to-Speech Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48933" target="_blank">Submitting Audio Noise Cancellation Job</a>


#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).

## Samples

#### Using multiple template IDs

#### Request

```shell
POST /jobs HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Input>
        <Object>input/demo.mp4</Object>
    </Input>
    <Operation>
        <Tag>Animation</Tag>
        <TemplateId>t1f16e1dfbdc994105b31292d45710642a</TemplateId>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/animation.gif</Object>
        </Output>
        <UserData>This is my Animation job.</UserData>
    </Operation>
    <Operation>
        <Tag>Transcode</Tag>
        <TemplateId>t1995d523e42df4c5e858f244b4174360c</TemplateId>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/transcode.mp4</Object>
        </Output>
        <UserData>This is my Trancode job.</UserData>
    </Operation>
    <Operation>
        <Tag>SmartCover</Tag>
        <SmartCover>
            <Format>jpg</Format>
            <Width>1280</Width>
            <Height>960</Height>
            <Count>5</Count>
            <DeleteDuplicates>true</DeleteDuplicates>
        </SmartCover>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/smartcover-${Number}.jpg</Object>
        </Output>   
        <UserData>This is my SmartCover job.</UserData>
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
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>j682b9662f84611ecb8546d80f2baf56f</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T15:23:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <Tag>Animation</Tag>
            <TemplateId>t1f16e1dfbdc994105b31292d45710642a</TemplateId>
            <TemplateName>animation_demo</TemplateName>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>output/animation.gif</Object>
            </Output>
            <UserData>This is my Animation job.</UserData>
        </Operation>
    </JobsDetail>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>j68427030f84611ecb8546d80f2baf56f</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T15:23:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <Tag>Transcode</Tag>
            <TemplateId>t1995d523e42df4c5e858f244b4174360c</TemplateId>
            <TemplateName>trancode_demo</TemplateName>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>output/transcode.mp4</Object>
            </Output>
            <UserData>This is my Trancode job.</UserData>
        </Operation>
    </JobsDetail>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>j6842765cf84611ecb8546d80f2baf56f</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T15:23:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <Tag>SmartCover</Tag>
            <SmartCover>
                <Format>jpg</Format>
                <Width>1280</Width>
                <Height>960</Height>
                <Count>5</Count>
                <DeleteDuplicates>true</DeleteDuplicates>
            </SmartCover>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>output/smartcover-${Number}.jpg</Object>
            </Output>   
            <UserData>This is my SmartCover job.</UserData>
        </Operation>
    </JobsDetail>
</Response>
```
