## Feature Description

The image moderation API supports both sync and async GET request methods. You can use this API to perform content moderation on an image file.

The API supports the following operations:

>!
> - Moderate image files stored in COS.
> - Moderate images at URLs of a third-party cloud storage vendor.
> - Local image files can be moderated after being Base64-encoded by calling the API for [batch image moderation](https://intl.cloud.tencent.com/document/product/436/48538).
> 

- Detect image files stored in COS or at URLs and recognize non-compliant content that may be offensive, unsafe, or inappropriate based on the deep learning technology.
- Moderate GIF images by capturing frames.
- Recognize various non-compliant scenes, including vulgar, illegal, pornographic, and adverting information.
- Detect various objects (such as object, advertising logo, and QR code) and recognize text in images through OCR.
  <span id=1></span>
- [Customize moderation policies](https://intl.cloud.tencent.com/document/product/436/52095) based on different business scenarios.
- Customize risk libraries to filter non-compliant content of custom types.

## Billing Description

- Each moderation scene is billed separately. For example, if you choose to moderate two scenes involving pornography and advertising, then **one image file** will be moderated and billed **twice**.
- Calling the API will incur image moderation fees and COS read request fees as described in [Request Fees](https://intl.cloud.tencent.com/document/product/436/40100).
- If the image files are stored in COS STANDARD_IA storage class, calling the moderation API will incur STANDARD_IA data retrieval fees as described in [Data Retrieval Fees](https://intl.cloud.tencent.com/document/product/436/40097).
- Image moderation is not supported for objects stored in the ARCHIVE or DEEP ARCHIVE storage classes. To moderate these objects, you first need to restore them as instructed in [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633).
- Moderating audios at URLs of a third-party cloud storage vendor will incur downstream traffic fees charged by the vendor.

## Restrictions

- Supported image file size: < 32 MB. To moderate images larger than 5 MB in size, you need to use the `large-image-detect` parameter when calling the API.
- Supported image file resolution: A **resolution above 256x256** is recommended; otherwise, the recognition effect may be affected.
- Supported image formats: PNG, JPG, JPEG, BMP, GIF, WEBP.
- Supported image URL transfer protocols: HTTP, HTTPS.
- Calling the API requires a signature. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

## SDK Recommendation

COS SDK provides complete capabilities of demo, automatic integration, and signature calculation. You can easily and quickly call APIs through the SDK. For more information, see [SDK Overview](https://intl.cloud.tencent.com/document/product/436/6474).

## Request

#### Sample request

```plaintext
GET /<ObjectKey>?ci-process=sensitive-content-recognition&detect-type=<type>&detect-url=<detect-url>&interval=<interval>&max-frames=<max-frames>&biz-type=<biz-type> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>?
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request parameters

The parameters are as described below:

| Parameter | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------ | -------- |
| ObjectKey          | Name of the image file in the COS bucket. The COS bucket is specified by `Host`. For example, if the file is `img.jpg` in the `test` directory in the `examplebucket-1250000000` bucket in Beijing, then `Host` is `examplebucket-1250000000.cos.ap-beijing.myqcloud.com`, and `ObjectKey` is `test/img.jpg`. | String | No |
| ci-process         | This field identifies the data processing feature, which is `sensitive-content-recognition` for content moderation. | String | Yes |
| biz-type           | Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as pornographic, adverting, and illegal information. For configuration guidelines, see [Setting Moderation Policy](#1). You can get `biz-type` in the console. If `biz-type` is specified, the moderation request will perform moderation based on the scenes configured in the moderation policy. If `biz-type` is not specified, the default moderation policy will be used automatically. | String | No       |
| detect-type        | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). This parameter will no longer be maintained in the future. You can pass in multiple types and separate them by comma, such as `Porn,Ads`. If you need to moderate more scenes, use the `biz-type` parameter. | String | No       |
| detect-url         | You can enter a `detect-url` value to moderate an image accessible over the public network. If `detect-url` is not specified, the backend will moderate by `ObjectKey` by default. If `detect-url` is specified, the backend will moderate by `detect-url`, and there will be no need to enter `ObjectKey`. Sample `detect-url`: http://www.example.com/abc.jpg.  | String | No      |
| interval           | For GIF image moderation, you can use this parameter to configure the frame capturing interval. The default value is `5`, indicating to capture a frame every five frames starting from the first frame (included). | Int | No |
| max-frames         | The maximum number of frames to be captured for GIF image moderation, which must be greater than 0. The default value is `5`, indicating to capture five frames at most. | Int | No |
| large-image-detect | Whether to compress the image that exceeds the size limit before moderation. Valid values: `0` (no), `1` (yes). Default value: `0`. Note: Images up to 32 MB in size can be compressed, and image compression fees will be charged. For large animated images such as GIF, the compression time is long, which may cause the moderation to fail due to timeout. | Int | No |
| dataid | Image ID. This field will return the original content in the result, which can contain up to 512 bytes. | String | No |
| async | Whether to moderate asynchronously. Valid values: `0` (returns the result synchronously); `1` (moderates asynchronously). Default value: `0`.  | Int    | No       |
| callback | The moderation result (in `Detail` mode) can be sent to your callback address in the form of a callback. This parameter takes effect for async moderation. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`.  | String | No |

>!
> - Moderation through `ObjectKey` is a private network operation and will not generate public network traffic.
> - Moderation through `detect-url` will generate public network traffic with regard to the origin where the image resides.
> 

#### Request body

The request body of this request is empty.

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

```plaintext
<RecognitionResult>
      <JobId>xxxxxxxxxxxxxxx</JobId>
      <Result>1</Result>
      <Label>Porn</Label>
      <SubLabel>SexBehavior</SubLabel>
      <Score>90</Score>
      <PornInfo>
          <Code>0</Code>
          <Msg>OK</Msg>
          <HitFlag>1</HitFlag>
          <Label>xxx</Label>
          <SubLabel>SexBehavior</SubLabel>
          <Score>100</Score>
          <OcrResults>
            <Text></Text>
            <Keywords></Keywords>
            <Location>
              <X></X>
              <Y></Y>
              <Width></Width>
              <Height></Height>
              <Rotate></Rotate>
            </Location>
          </OcrResults>
      </PornInfo>
</RecognitionResult>
```

The response body is as described below:

| Parameter | Type | Description |
| ----------------- | --------- | ------------ |
| RecognitionResult | Container | Image moderation result. |

Content of `RecognitionResult` for async moderation:

| Parameter | Type | Description |
| -------- | ------ | -------------------------------------------------------- |
| DataId            | String    | Image ID. The original content will be returned in the moderation result, which can contain up to 512 bytes.        |
| JobId             | String    | Image moderation job ID.                                          |
| State             | String    | Status of the moderation job. Valid value: `Submitted`. |
| Object            | String    | The name of the image stored in the COS bucket, which will be returned if `ObjectKey` is selected during job creation.  |
| Url               | String    | The URL of the image file, which will be returned if `detect-url` is selected during job creation.                    |

Content of `RecognitionResult` for sync moderation:

| Parameter | Type | Description |
| ----------------- | --------- | ------------------------------------------------------------ |
| DataId            | String    | Image ID. The original content will be returned in the moderation result, which can contain up to 512 bytes.        |
| JobId             | String    | Image moderation job ID.                                          |
| State             | String    | Status of the moderation job. Valid value: `Success`. |
| Object            | String    | The name of the image stored in the COS bucket, which will be returned if `ObjectKey` is selected during job creation.  |
| Url               | String    | The URL of the image file, which will be returned if `detect-url` is selected during job creation.                    |
| CompressionResult | Int   | Whether the image is compressed. Valid values: `0` (no), `1` (yes).        |
| Result            | Int       | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results based on your business needs. Valid values: `0` (normal), `1` (sensitive), and `2` (suspiciously sensitive, with human review recommended). |
| Label             | String    | This field is used to return the **maliciousness tag with the highest priority** in the detection result, which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions based on your business needs. Returned values: `Normal`, `Porn`, `Ads`, and other types of unsafe or inappropriate content. |
| Category          | String    | This field is a subset of `Label`, indicating the specific moderation category hit; for example, `Sexy` presents the sexy category in the `Porn` tag. |
| SubLabel          | String    | Second-level tag hit by the image.                                       |
| Score      | Int         | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. For example, `Porn 99` means that the content is very likely to be pornographic. |
| Text              | String    | The specific text content recognized by OCR in the image, which will be returned if text content detection is enabled in the moderation policy.    |
| PornInfo          | Container | The moderation result of the **pornographic information** moderation scene.                             |
| AdsInfo           | Container | The moderation result of the **advertising information** moderation scene.                         |

The moderation information (`PornInfo` and `AdsInfo`) has the following sub-nodes:

| Parameter | Type | Description |
| ---------- | --------------- | ------------------------------------------------------------ |
| Code       | Int             | Error code. `0` indicates a success, while other numbers correspond to different errors. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700). |
| Msg        | String          | The specific error message, which will be `OK` if the moderation result is normal. |
| HitFlag    | Int         | The moderation result returned for the moderation scene. Returned values: `0` (normal); `1` (confirmed as a violation of the current scene); `2` (suspected as a violation of the current scene).   |
| Score      | Int         | The confidence the moderation result hits the moderation scene. Value range: 0–100. The higher the value, the more likely the content hits the currently returned moderation scene. A value in the range of 0–60, 61–90, or 91–100 means the image is normal, suspiciously sensitive, or sensitive respectively. For example, `Porn 99` means that the content is very likely to be pornographic.  |
| Label      | String          | This field indicates the overall result tag of the screenshot, which may be `SubLabel`, a person name, etc. |
| Category          | String    | This field is a subset of `Label`, indicating the specific moderation category hit; for example, `Sexy` presents the sexy category in the `Porn` tag. |
| SubLabel   | String          | This field indicates the specific sub-tag hit by the moderation job; for example, `SexBehavior` is a sub-tag under the `Porn` tag. Note: This field may return null, indicating that no specific sub-tags are hit. |
| OcrResults | Container Array | This field represents the detailed OCR result, including the text recognition result and hit keyword. It will be returned if there is non-compliant content. |
| LibResults | Container Array | This field returns results based on recognition against the risk library. Note: This field will not be returned if no samples in the risk library are hit. |

`LibResults` has the following sub-nodes:

| Parameter | Type | Description |
| -------- | ------- | ------------------------------------------------------- |
| ImageId  | String  | This field represents the hit image sample ID in the risk library.                       |
| Score    | Integer | This field returns the confidence under the current tag. Value range: 0–100.  The higher the value, the more likely the image hits a sample in the risk library.  For example, `Porn 99` means that the content is very likely to hit a pornographic sample in the library.  |

`OcrResults` has the following sub-nodes:

| Parameter | Type | Description |
| -------- | ------------ | ------------------------------------------------------------ |
| Text     | String       | The specific text content recognized by OCR in the image.                            |
| Keywords | String Array | Keywords hit by the current moderation scene.                                 |
| Location | Container    | This parameter is used to return the position (X and Y coordinates of the top-left corner, length, width, and rotation angle) of the OCR detection frame in the image for quick location of the recognized text. |

`Location` has the following sub-nodes:

| Parameter | Type | Description |
| :----- | :---- | :----------------------------------------------------------- |
| X      | Float | This parameter is used to return the pixel position of the **abscissa (X) of the top-left corner** of the detection frame. It can be combined with other parameters to uniquely determine the size and position of the detection frame. |
| Y      | Float | This parameter is used to return the pixel position of the **ordinate of the top-left corner** (Y) of the detection frame. It can be combined with other parameters to uniquely determine the size and position of the detection frame. |
| Width  | Float | This parameter is used to return the **width of the detection frame** (the length starting from the top-left corner and extending to the right on the X axis). It can be combined with other parameters to uniquely determine the size and position of the detection frame. |
| Height | Float | This parameter is used to return the **height of the detection frame** (the length starting from the top-left corner and extending down the Y axis). It can be combined with other parameters to uniquely determine the size and position of the detection frame. |
| Rotate | Float | This parameter is used to return the **rotation angle of the detection frame**. Valid values: **0–360** (**degrees**), and the direction is **counterclockwise rotation**. This parameter can be combined with the `X` and `Y` coordinate parameters to uniquely determine the specific position of the detection frame. |

`ObjectResults` has the following sub-nodes:

| Parameter | Type | Description |
| :------- | :-------- | :----------------------------------------------------------- |
| Name     | String    | This field is used to return the name of the recognized object, such as person name.                 |
| Location | Container | This parameter is used to return the position (X and Y coordinates of the top-left corner, length, width, and rotation angle) of the recognition result in the image for you to quickly locate information. |

## Samples

#### Request 1: Sync image moderation

```plaintext
GET /picture.jpg?ci-process=sensitive-content-recognition&detect-type=porn&interval=0&max-frames=1&biz-type=*** HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Date: Tue, 03 Apr 2019 09:06:15 GMT
Authorization:XXXXXXXXXXXX
```

#### Response 1

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 645
Date: Tue, 03 Apr 2018 09:06:16 GMT
Status: 200 OK
x-cos-request-id: NWFjMzQ0MDZfOTBmYTUwXzZkZV8z****

<RecognitionResult>
      <JobId>xxxxxxxxxxxxxxx</JobId>
      <CompressionResult>0</CompressionResult>
      <Result>1</Result>
      <Label>Porn</Label>
      <SubLabel>SexBehavior</SubLabel>
      <Score>95</Score>
      <PornInfo>
          <Code>0</Code>
          <Msg>OK</Msg>
          <HitFlag>1</HitFlag>
          <Label>xxx</Label>
          <SubLabel>SexBehavior</SubLabel>
          <Score>95</Score>
      </PornInfo>
</RecognitionResult>
```

#### Request 2: Async image moderation

```plaintext
GET /picture.jpg?ci-process=sensitive-content-recognitionbiz-type=***&async=1&callback=http://www.callback.com HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Date: Tue, 03 Apr 2019 09:06:15 GMT
Authorization:XXXXXXXXXXXX
```

#### Response 2

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 645
Date: Tue, 03 Apr 2018 09:06:16 GMT
Status: 200 OK
x-cos-request-id: NWFjMzQ0MDZfOTBmYTUwXzZkZV8z****

<RecognitionResult>
      <JobId>xxxxxxxxxxxxxxx</JobId>
</RecognitionResult>
```
