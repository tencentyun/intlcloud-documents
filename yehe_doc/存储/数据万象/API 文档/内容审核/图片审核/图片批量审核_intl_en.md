## Feature Description

The batch image moderation API can adopt either sync or async POST request method. You can use this API to perform content moderation on multiple image files.

>?
> - Moderate image files stored in COS.
> - Moderate images at URLs of a third-party cloud storage vendor.
> 

<span id=1></span>
Customize moderation policies based on different business scenarios as instructed in [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/1045/52107).

## Restrictions

- Supported image file size: < 32 MB. To moderate images larger than 5 MB in size, you need to use the `large-image-detect` parameter when calling the API.
- Supported image quantity: Up to **100** images per request.
- Supported image file resolution: A **resolution above 256x256** is recommended; otherwise, the recognition effect may be affected.
- Supported image formats: PNG, JPG, JPEG, BMP, GIF, WEBP.
- Supported image URL transfer protocols: HTTP, HTTPS.
- Calling the API requires a signature. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

## SDK Recommendation

COS SDK provides complete capabilities of demo, automatic integration, and signature calculation. You can easily and quickly call APIs through the SDK. For more information, see [SDK Overview](https://intl.cloud.tencent.com/document/product/436/6474).

## Request

#### Sample request

```plaintext
POST /image/auditing HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>?
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```plaintext
<Request>
    <Input>
      <DataId></DataId>
      <Url></Url>
      <Object></Object>
      <Content></Content>
      <Interval></Interval>
      <MaxFrames></MaxFrames>
      <LargeImageDetect></LargeImageDetect>
      <UserInfo>
        <TokenId></TokenId>
      </UserInfo>
    </Input>
    <Input>
      <DataId></DataId>
      <Url></Url>
      <Object></Object>
      <Content></Content>
      <Interval></Interval>
      <MaxFrames></MaxFrames>
    </Input>
    <Conf>
      <DetectType>Porn,Ads</DetectType>
      <BizType>b81d45f94b91a683255e9a9506f45a11</BizType>
      <Async></Async>
      <Callback></Callback>
    </Conf>
</Request>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :------------------------- | :-------- | :--- |
| Request | None | Batch image moderation configuration. | Container | Yes |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :-------------------------------------------------- | :-------------- | :--- |
| Input | Request | Content to be moderated. If there are multiple images, pass in multiple `Input` structures. | Container Array | Yes |
| Conf | Request | Moderation rule configuration. | Container | Yes |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :----------------------------------------------------------- | :----- | :--- |
| Object | Request.Input | Name of the image file stored in the COS bucket; for example, if the file is `image.jpg` in the `test` directory, then the filename is `test/image.jpg`. If multiple parameters among `Content`, `Object`, and `Url` are passed in, only one will take effect in the order of `Content` > `Object` > `Url`.  | String | No |
| Url | Request.Input | Full URL of the image file, such as `http://a-1250000.cos.ap-shanghai.myqcloud.com/image.jpg`. If multiple parameters among `Content`, `Object`, and `Url` are passed in, only one will take effect in the order of `Content` > `Object` > `Url`.  | String | No |
| Content            | Request.Input | Image file content, which needs to be Base64-encoded first. If multiple parameters among `Content`, `Object`, and `Url` are passed in, only one will take effect in the order of `Content` > `Object` > `Url`.  | String | No |
| Interval | Request.Input | Frame capturing frequency, which takes effect for GIF images only. The default value is `5`, indicating to capture a frame every five frames starting from the first frame (included). | Int | No |
| MaxFrames | Request.Input | The maximum number of frames to be captured, which takes effect for GIF images only. The default value is `5`, indicating to capture only five frames of the GIF image for moderation. The parameter value must be greater than 0. | Int | No |
| DataId | Request.Input | Image ID. This field will return the original content in the result, which can contain up to 512 bytes. | String | No |
| LargeImageDetect | Request.Input | Whether to compress the image that exceeds the size limit before moderation. Valid values: `0` (no), `1` (yes). Default value: `0`. Note: Images up to 32 MB in size can be compressed, and compression fees will be charged.  | Int | No |
| UserInfo | Request.Input | Business field. | Container | No |

`UserInfo` has the following sub-nodes:

| Node Name (Keyword) | Description | Type | Required |
| :----------------- | :-------------------------------------------------- | :----- | :------- |
| TokenId            | Account information, which can contain up to 128 bytes.           | String | No       |
| Nickname           | Nickname information, which can contain up to 128 bytes.           | String | No       |
| DeviceId           | Device information, which can contain up to 128 bytes.           | String | No       |
| AppId              | Unique app ID, which can contain up to 128 bytes.           | String | No       |
| Room               | Room ID information, which can contain up to 128 bytes.           | String | No       |
| IP                 | IP address information, which can contain up to 128 bytes.           | String | No       |
| Type               | Business type, which can contain up to 128 bytes.           | String | No       |
| ReceiveTokenId     | User account to receive messages, which can contain up to 128 bytes.           | String | No       |
| Gender             | Gender information, which can contain up to 128 bytes.           | String | No       |
| Level              | Level information, which can contain up to 128 bytes.           | String | No       |
| Role               | Role information, which can contain up to 128 bytes.           | String | No       |

`Conf` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------- | :----------------------------------------------------------- | :----- | :--- |
| BizType | Request.Conf | Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as pornographic, adverting, and illegal information. For configuration guidelines, see [Setting Moderation Policy](#1). You can get `BizType` in the console. If `BizType` is specified, the moderation request will perform moderation based on the scenes configured in the moderation policy. If `BizType` is not specified, the default moderation policy will be used automatically. | String | No |
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). This parameter will no longer be maintained in the future. You can pass in multiple types and separate them by comma, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter. | String | No |
| Async | Request.Conf | Whether to moderate asynchronously. Valid values: `0` (returns the result synchronously); `1` (moderates asynchronously). Default value: `0`.  | Integer | No |
| Callback | Request.Conf | The moderation result (in `Detail` mode) can be sent to your callback address in the form of a callback. This parameter takes effect for async moderation. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`.  | String | No |

>!
> - Moderation through `Object` is a private network operation and will not generate public network traffic.
> - Moderation through `Url` will generate public network traffic with regard to the origin where the image resides.
> 

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
  <JobsDetail>
    <DataId></DataId>
    <Url></Url>
    <PornInfo>
      <HitFlag>1</HitFlag>
      <Score>100</Score>
      <Category>xxx</Category>
      <SubLabel>xxx</SubLabel>
    </PornInfo>
  </JobsDetail>
  <JobsDetail>
    <Code>InvalidArgument</Code>
    <Message>Param MaxFrames is illegal</Message>
    <DataId></DataId>
  </JobsDetail>
</Response>
```

The response body is as described below:

| Node Name (Keyword) | Parent Node | Description |
| :----------------- | :-------- | :----------------------------- |
| Response           | Container | The specific response content returned by batch image moderation. |

`Response` has the following sub-nodes:

| Parameter | Type | Description |
| :--------- | :-------------- | :----------------------------------------------------------- |
| JobsDetail | Container Array | Image moderation result.                                               |
| RequestId  | String          | The ID automatically generated by the server for a request when the request is sent, which can help locate problems faster. |

The async moderation result `JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Type | Description |
| :----------------- | :----- | :----------------------------------------------------------- |
| Code              | String    | Error code, which will be returned only in case of a failure. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700). |
| Message           | String    | Error message, which will be returned only in case of a failure.        |
| DataId            | String    | Image ID. The original content will be returned in the moderation result, which can contain up to 512 bytes.        |
| JobId             | String    | Moderation job ID.                                          |
| State             | String    | Status of the moderation job. Valid values: `Submitted`, `Failed`. |
| Object            | String    | The name of the image file stored in the COS bucket, which will be returned if `Object` is selected during job creation.  |
| Url               | String    | The URL of the image file, which will be returned if `Url` is selected during job creation.                    |

The sync moderation result `JobsDetail` has the following sub-nodes:

| Parameter | Type | Description |
| :---------------- | :-------- | :----------------------------------------------------------- |
| Code              | String    | Error code, which will be returned only in case of a failure. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700). |
| Message           | String    | Error message, which will be returned only in case of a failure.        |
| DataId            | String    | Image ID. The original content will be returned in the moderation result, which can contain up to 512 bytes.        |
| JobId             | String    | Moderation job ID.                                          |
| State             | String    | Status of the moderation job. Valid values: `Success`, `Failed`. |
| Object            | String    | The name of the image file stored in the COS bucket, which will be returned if `Object` is selected during job creation.  |
| Url               | String    | The URL of the image file, which will be returned if `Url` is selected during job creation.                    |
| CompressionResult | Integer   | Whether the image is compressed. Valid values: `0` (no), `1` (yes).        |
| Label             | String    | This field is used to return the **maliciousness tag with the highest priority** in the detection result, which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions based on your business needs. Returned values: `Normal`, `Porn`, `Ads`. |
| Result            | Integer   | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results based on your business needs. Valid values: `0` (normal), `1` (sensitive), and `2` (suspiciously sensitive, with human review recommended). |
| Score      | Integer         | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. For example, `Porn 99` means that the content is very likely to be pornographic. |
| Category          | String    | Moderation type hit by the image.                                     |
| SubLabel          | String    | Second-level tag hit by the image.                                       |
| Text              | String    | The specific text content recognized by OCR in the image, which will be returned if text content detection is enabled in the moderation policy.    |
| PornInfo          | Container | The moderation result of the **pornographic information** moderation scene.                             |
| AdsInfo           | Container | The moderation result of the **advertising information** moderation scene.                         |
| UserInfo          | Container | `UserInfo` set in the request, which will be returned as-is.                                 |
| ListInfo          | Container | Blocklist/Allowlist status of the account.                                           |

The moderation information (such as `PornInfo` and `AdsInfo`) has the following sub-nodes:

| Parameter | Type | Description |
| :--------- | :-------------- | :----------------------------------------------------------- |
| Code       | Integer         | Error code for individual moderation scenes. 0: Succeeded; other values: Failed. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700). |
| Msg        | String          | The specific error message, which will be `OK` if the moderation result is normal. |
| HitFlag    | Integer         | The moderation result returned for the moderation scene. Returned values: `0` (normal); `1` (confirmed as a violation of the current scene); `2` (suspected as a violation of the current scene).   |
| Score      | Integer         | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. For example, `Porn 99` means that the content is very likely to be pornographic. |
| Label      | String          | The overall result tag of the image, which may be `SubLabel`, a person name, etc. |
| Category          | String    | This field is a subset of `Label`, indicating the specific moderation category hit; for example, `Sexy` presents the sexy category in the `Porn` tag. |
| SubLabel   | String          | Second-level tag of the image.                                           |
| OcrResults | Container Array | This field represents the detailed OCR result, including the text coordinate information and text recognition result. It will be returned if there is non-compliant content. |
| LibResults | Container Array | This field returns results based on recognition against the risk library. Note: This field will not be returned if no samples in the risk library are hit. |

`LibResults` has the following sub-nodes:

| Node Name (Keyword) | Type | Description |
| :----------------- | :----------- | :--------------------------- |
| ImageId  | String  | This field represents the hit image sample ID in the risk library.                       |
| Score              | Integer      | This field returns the confidence under the current tag. Value range: 0–100.  The higher the value, the more likely the image hits a sample in the risk library.  For example, `Porn 99` means that the content is very likely to hit a pornographic sample in the library. |

`OcrResults` has the following sub-nodes:

| Node Name (Keyword) | Type | Description |
| :----------------- | :----------- | :--------------------------- |
| Text               | String       | Sensitive OCR text content   |
| Keywords           | String Array | Sensitive words in the text content       |
| Location           | Container    | Location information of the text content in the image |

`ObjectResults` has the following sub-nodes:

| Node Name (Keyword) | Type | Description |
| :----------------- | :-------- | :------------------------- |
| Name               | String    | Sensitive content name.           |
| Location           | Container | Location information of the content in the image. |

`Location` has the following sub-nodes:

| Node Name (Keyword) | Type | Description |
| :----------------- | :------ | :-------------------------------- |
| X | Float | X-coordinate relative to the origin (top-left corner of the image). |
| Y | Float | Y-coordinate relative to the origin (top-left corner of the image). |
| Height | Float | Height of the sensitive area. |
| Width | Float | Width of the sensitive area. |
| Rotate | Float | Rotation angle of the sensitive area. |

`UserInfo` has the following sub-nodes (same as the `UserInfo` in the request):

| Node Name (Keyword) | Description | Type | Required |
| :----------------- | :-------------------------------------------------- | :----- | :------- |
| TokenId            | Account information, which can contain up to 128 bytes.           | String | No       |
| Nickname           | Nickname information, which can contain up to 128 bytes.           | String | No       |
| DeviceId           | Device information, which can contain up to 128 bytes.           | String | No       |
| AppId              | Unique app ID, which can contain up to 128 bytes.           | String | No       |
| Room               | Room ID information, which can contain up to 128 bytes.           | String | No       |
| IP                 | IP address information, which can contain up to 128 bytes.           | String | No       |
| Type               | Business type, which can contain up to 128 bytes.           | String | No       |
| ReceiveTokenId     | User account to receive messages, which can contain up to 128 bytes.           | String | No       |
| Gender             | Gender information, which can contain up to 128 bytes.           | String | No       |
| Level              | Level information, which can contain up to 128 bytes.           | String | No       |
| Role               | Role information, which can contain up to 128 bytes.           | String | No       |

`ListInfo` has the following sub-nodes:

| Node Name (Keyword) | Type | Description |
| :---------------- | :-------------- | :------------------------------------------------------ |
| ListResults       | Container Array | Results in all hit lists. |

`ListResults` has the following sub-nodes:

| Node Name (Keyword) | Type | Description |
| :---------------- | :------ | :------------------------------------------------------ |
| ListType          | Integer | Type of the hit list. Valid values: `0` (allowlist), `1` (blocklist). |
| ListName          | String  | Name of the hit list.                                 |
| Entity            | String  | Entity hit in the list.                         |

## Samples

#### Request

```plaintext
POST /image/auditing HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
  <Input>
    <Object>a.jpg</Object>
  </Input>
  <Input>
    <Url>http://exsample.com/b.jpg</Url>
  </Input>
  <Conf>
    <DetectType>Porn,Ads</DetectType>
  </Conf>
</Request>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 645
Date: Tue, 03 Apr 2018 09:06:16 GMT
Status: 200 OK
x-cos-request-id: NWFjMzQ0MDZfOTBmYTUwXzZkZV8z****

<Response>
    <JobsDetail>
        <JobId>xxxxxxxxxx</JobId>
        <CompressionResult>0</CompressionResult>
        <Object>a.jpg</Object>
        <Label>Porn</Label>
        <Result>1</Result>
        <Score>100</Score>
        <SubLabel>xxx</SubLabel>
        <PornInfo>
            <Code>0</Code>
            <Msg>OK</Msg>
            <HitFlag>1</HitFlag>
            <Score>100</Score>
            <Label>xxx</Label>
            <SubLabel>xxx</SubLabel>
        </PornInfo>
    </JobsDetail>
    <JobsDetail>
        <JobId>yyyyyyyyyy</JobId>
        <CompressionResult>0</CompressionResult>
        <Url>http://exsample.com/b.jpg</Url>
        <Label>Porn</Label>
        <Result>1</Result>
        <Score>100</Score>
        <SubLabel>xxx</SubLabel>
        <PornInfo>
            <Code>0</Code>
            <Msg>OK</Msg>
            <HitFlag>1</HitFlag>
            <Score>100</Score>
            <Label>xxx</Label>
            <SubLabel>xxx</SubLabel>
        </PornInfo>
    </JobsDetail>
    <RequestId>xxxxxxxxxxx</RequestId>
</Response>
```
