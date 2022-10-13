## Feature Description

This API is used to update a splicing template.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateConcatTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
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
PUT /template/<TemplateId> HTTP/1.1
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

#### Common request headers

This API uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Non-common request headers

This request operation does not use any non-common request headers.

#### Request body

This request requires the following request body:

```shell
<Request>
    <Tag>Concat</Tag>
    <Name>TemplateName</Name>
    <ConcatTemplate>
        <ConcatFragment>
            <Mode>Start</Mode>
            <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/start.mp4</Url>
        </ConcatFragment>
        <ConcatFragment>
            <Mode>End</Mode>
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
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Request            | None     | <a href="https://intl.cloud.tencent.com/document/product/1045/49907" target="_blank">Same as `Request` in the splicing template creation API.</a> | Container | 

## Response

#### Response headers

#### Common response headers

This response contains common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Non-common response headers

This response does not use any non-common response header.

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Tag>Concat</Tag>
        <Name>TemplateName</Name>
        <ConcatTemplate>
            <ConcatFragment>
                <Mode>Start</Mode>
                <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/start.mp4</Url>
            </ConcatFragment>
            <ConcatFragment>
                <Mode>End</Mode>
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
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :----------------------------------------------------- | :-------- |
| Response           | None     | <a href="https://intl.cloud.tencent.com/document/product/1045/49907" target="_blank">Same as `Response` in the splicing template creation API.</a> | Container |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).

## Samples

#### Request

```shell
PUT /template/t1460606b9752148c4ab182f55163ba7cd HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98****-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml

<Request>
    <Tag>Concat</Tag>
    <Name>TemplateName</Name>
    <ConcatTemplate>
        <ConcatFragment>
            <Mode>Start</Mode>
            <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/start.mp4</Url>
        </ConcatFragment>
        <ConcatFragment>
            <Mode>End</Mode>
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
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzh****=

<Response>
    <Template>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Tag>Concat</Tag>
        <Name>TemplateName</Name>
        <ConcatTemplate>
            <ConcatFragment>
                <Mode>Start</Mode>
                <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/start.mp4</Url>
            </ConcatFragment>
            <ConcatFragment>
                <Mode>End</Mode>
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
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```
