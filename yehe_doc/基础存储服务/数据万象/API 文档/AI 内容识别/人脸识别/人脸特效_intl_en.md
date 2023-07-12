## Feature Description

Face filter supports beauty filter, gender swap, age change, and face cut-out. It is suitable for many use cases, such as social entertainment, marketing, and interactive communication.

| Feature | Description |
| ------------ | ------------------------------------------------------------ |
| Beauty filter     | You can upload a selfie and quickly apply smart skin brightening, skin smoothing, face slimming, eye enlarging, and contouring filters. You can also customize parameters. |
| Gender swap | You can upload a face image and have the gender swapped based on the face editing and generation algorithms. Beauty filters, makeup, bang, and long hair can be added to a face swapped from male to female, while beard and short hair can be added to a face swapped from female to male. |
| Age change | You can upload a face image and make the face look older or younger based on the face editing and generation algorithms. |
| Face cut-out     | You can upload an image and get the body contour recognized and separated from the background. The binary image, grayscale image, and foreground portrait are returned. This is applicable to portrait keying, photo synthesis, face special effect, and other use cases and greatly improves the tool efficiency. |

>?
>- Face filters can be applied to a Base64-encoded image of up to 5 MB in size. PNG, JPG, JPEG, and BMP formats are supported, while GIF is not. To use face cut-out, the image resolution must be lower than 2000x2000 px.
>- Face filter is a paid service. For billing details, see Content Recognition Fees.
>- This feature currently can be used only through APIs.

## Request

#### Sample request

```plaintext
GET /<ObjectKey>?ci-process=face-effect&type=<type> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>

```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see Authorization Granularity.
> 

#### Request parameters

| Parameter | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------- | -------- |
| ObjectKey | Object name, such as `folder/document.jpg`. | String  | Yes |
| ci-process | CI's processing capability, which is fixed at `face-effect` for face filter. | String | Yes |
| type         | Face filter type. Valid value: face-beautify, face-gender-transformation, face-age-transformation, face-segmentation. | String  | Yes       |
| whitening    | Skin brightening level, which takes effect if `type` is `face-beautify`. Value range: [0,100]. Default value: 30. The higher the value, the more obvious the effect. | Integer | No       |
| smoothing    | Skin smoothing level, which takes effect if `type` is `face-beautify`. Value range: [0,100]. Default value: 10. The higher the value, the more obvious the effect. | Integer | No       |
| faceLifting    | Face slimming level, which takes effect if `type` is `face-beautify`. Value range: [0,100]. Default value: 70. The higher the value, the more obvious the effect. | Integer | No       |
| eyeEnlarging | Eye enlarging level, which takes effect if `type` is `face-beautify`. Value range: [0,100]. Default value: 70. The higher the value, the more obvious the effect. | Integer | No       |
| gender       | Target gender, which takes effect if `type` is `face-gender-transformation`. 0: male to female; 1: female to male. There is no default value. Note that only the gender of the largest face in the image will be swapped. | Integer | Yes       |
| age          | Target age, which takes effect if `type` is `face-age-transformation`. Value range: [10, 80]. There is no default value. Note that only the age of the largest face in the image will be changed. | Integer | Yes       |



#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request does not have a request body.

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610). 

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
  <ResultImage>Base64-encoded image</ResultImage>
  <ResultMask>Base64-encoded file</ResultMask>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------------------------------------- | :----- |
| ResultImage        | Response | Base64-encoded result image data                                     | String |
| ResultMask         | Response | Face cut-out output parameter, which is a Base64-encoded file consisting of floating point numbers after being decoded. These numbers represent pixels in each line starting from the top-left corner of the input image. The value of each number is the grayscale value (0–255) converted from the confidence (0–1) of the body contour. | String |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Request

```plaintext
GET /test.jpg?ci-process=face-effect&type=face-beautify&whitening=70&smoothing=80&faceLifting=70&eyeEnlarging=70 HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 414641
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-image
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
  <ResultImage>Base64-encoded image</ResultImage>
</Response>
```
