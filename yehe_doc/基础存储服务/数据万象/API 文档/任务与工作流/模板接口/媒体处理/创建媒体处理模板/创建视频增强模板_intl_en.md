## Feature Description

This API is used to create a video enhancement template.

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
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
>

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```shell
<Request>
    <Tag>VideoProcess</Tag>
    <Name>TemplateName</Name>
    <ColorEnhance>
        <Enable>true</Enable>
        <Contrast></Contrast>
        <Correction></Correction>
        <Saturation></Saturation>
    </ColorEnhance>
    <MsSharpen>
        <Enable>true</Enable>
        <SharpenLevel></SharpenLevel>
    </MsSharpen>
</Request>

```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | -------- |
| Request            | None     | Request container | Container | Yes       |

<span id="Request"></span>
`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | ---------------------------------------- | --------- | ------------------------------------------ | ---- |
| Tag                | Request | Template tag: VideoProcess                                | String    | Yes   | No |
| Name               | Request | Template name, which can contain letters, digits, underscores (_), hyphens (-), and asterisks (*).                    | String    | Yes   | None |
| ColorEnhance       | Request | Color enhancement                                          | Container | No. `ColorEnhance` and `MsSharpen` cannot be empty at the same time.  | None |
| MsSharpen       | Request | Detail enhancement                                          | Container | No. `ColorEnhance` and `MsSharpen` cannot be empty at the same time.  | None |

<span id="ColorEnhance"></span>
`ColorEnhance` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | -------------------- | ---------------- | ------ | -------- | ------ | ------------------------------------------- |
| Enable                    | Request.ColorEnhance | Whether to enable color enhancement       | String | None   | false     | true, false  |
| Contrast                  | Request.ColorEnhance | Contrast            | String | No   | None     | Value range: [0, 100] or a null string indicating automatic analysis  |
| Correction                | Request.ColorEnhance | Color correction           | String | No   | None     | Value range: [0, 1000] or a null string indicating automatic analysis  |
| Saturation                  | Request.ColorEnhance | Saturation            | String | No   | None     | Value range: [0, 300] or a null string indicating automatic analysis  |

<span id="MsSharpen"></span>
`MsSharpen` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ----------------- | ---------------- | ------ | -------- | ------ | ----------------------------------------- |
| Enable                    | Request.MsSharpen | Whether to enable detail enhancement       | String | None   | false     | true, false  |
| SharpenLevel      | Request.MsSharpen | Enhancement level    | String | No   | None    | Value range: [0, 10] or a null string indicating automatic analysis             |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <Tag>VideoProcess</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <VideoProcess>
            <ColorEnhance>
                <Enable>true</Enable>
                <Contrast></Contrast>
                <Correction></Correction>
                <Saturation></Saturation>
            </ColorEnhance>
            <MsSharpen>
                <Enable>true</Enable>
                <SharpenLevel></SharpenLevel>
            </MsSharpen>
        <VideoProcess>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

<span id="Response"></span>
`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------- | :----------------------------- | :-------- |
| TemplateId         | Response.Template | Template ID                        | String    |
| Name               | Response.Template | Template name                       | String    |
| BucketId           | Response.Template | Template bucket                 | String    |
| Category           | Response.Template | Template category: Custom or Official | String    |
| Tag                | Response.Template | Template tag: VideoProcess                                       | String    |
| UpdateTime         | Response.Template | Update time                       | String    |
| CreateTime         | Response.Template | Creation time                       | String    |
| VideoProcess       | Response.Template     | Template parameters                                                | Container |

<span id="VideoProcess"></span>
`VideoProcess` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description |
| :----------------- | :----------------------------- | :-------------------------------- |
| ColorEnhance       | Response.Template.VideoProcess | Same as the `Request.ColorEnhance` in the request body.  |
| MsSharpen          | Response.Template.VideoProcess | Same as the `Request.MsSharpen` in the request body.     |


#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).


## Samples

#### Request

```shell
POST /template HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml

<Request>
    <Tag>VideoProcess</Tag>
    <Name>TemplateName</Name>
    <ColorEnhance>
        <Enable>true</Enable>
        <Contrast></Contrast>
        <Correction></Correction>
        <Saturation></Saturation>
    </ColorEnhance>
    <MsSharpen>
        <Enable>true</Enable>
        <SharpenLevel></SharpenLevel>
    </MsSharpen>
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
        <Tag>VideoProcess</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <ColorEnhance>
            <Enable>true</Enable>
            <Contrast></Contrast>
            <Correction></Correction>
            <Saturation></Saturation>
        </ColorEnhance>
        <MsSharpen>
            <Enable>true</Enable>
            <SharpenLevel></SharpenLevel>
        </MsSharpen>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```
