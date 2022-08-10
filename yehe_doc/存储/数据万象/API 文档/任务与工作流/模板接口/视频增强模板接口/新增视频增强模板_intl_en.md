## Feature Description
This API (`CreateMediaTemplate`) is used to create a video enhancement template.

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

>? Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

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
| ------------------ | ------ | -------------- | --------- | ---- |
| Request            | None | Request container | Container | Yes   |


`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- | ---- |
| Tag                | Request | Task type: VideoProcess                                | String    | Yes   | No |
| Name               | Request | Template name. The value can contain only Chinese characters, letters, digits, underscores (_), hyphens (-), and asterisks (*).                    | String    | Yes   | None |
| ColorEnhance       | Request | Color enhancement                                          | Container | No. `ColorEnhance` and `MsSharpen` cannot be empty at the same time.  | None |
| MsSharpen       | Request | Detail enhancement                                          | Container | No. `ColorEnhance` and `MsSharpen` cannot be empty at the same time.  | None |


`ColorEnhance` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------------- | -------------------- | ------------------| ------ | ---- | ------ | ----- |
| Enable                    | Request.ColorEnhance | Whether to enable color enhancement       | String | None   | false     | true, false  |
| Contrast                  | Request.ColorEnhance | Contrast            | String | No   | None     | Value range: [0, 100] or null (a null string indicates automatic analysis)  |
| Contrast                  | Request.ColorEnhance | Color correction           | String | No   | None     | Value range: [0, 1000] or null (a null string indicates automatic analysis)  |
| Saturation                  | Request.ColorEnhance | Saturation            | String | No   | None     | Value range: [0, 300] or null (a null string indicates automatic analysis)  |

`MsSharpen` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ----------------- | ------------- | -------------- | ------ | ---- | ------ | ------------------ |
| Enable                    | Request.MsSharpen | Whether to enable detail enhancement       | String | None   | false     | true, false  |
| SharpenLevel      | Request.MsSharpen | Enhancement level    | String | No   | None    | Value range: [0, 10] or null (a null string indicates automatic analysis)             |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <Tag>VideoProcess</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
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

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :----------------------------------------------------- | :-------- |
| Response           | None | Response container | Container |


`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------------- | :----------------------------------------------------------- | :-------- |
| TemplateId         | Response.Template     | Template ID                                                      | String    |
| Name               | Response.Template     | Template name                                                     | String    |
| BucketId           | Response.Template     | Template bucket                                                | String    |
| Category           | Response.Template     | Template category: Custom or Official                                | String    |
| Tag                | Response.Template | Task type: VideoProcess                                       | String    |
| UpdateTime         | Response.Template     | Update time                                                     | String    |
| CreateTime         | Response.Template     | Creation time                                                     | String    |
| VideoProcess       | Response.Template     | Template parameters                                                | Container |


`VideoProcess` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | 
| :----------------- | :----------------------------- | :------------------------------- |
| ColorEnhance       | Response.Template.VideoProcess | Same as `Request.ColorEnhance` in the request body.  |
| MsSharpen          | Response.Template.VideoProcess | Same as `Request.MsSharpen` in the request body.     |


#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).


## Examples

#### Request

```shell
POST /template HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
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
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <Template>
        <Tag>VideoProcess</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
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
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```
