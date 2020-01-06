## Description
Backed by the persistence processing API of CI, the inventory scan feature of content recognition can be used to scan COS inventory data to recognize images containing pornographic, political, violent, terroristic, or advertising content. The content recognition request is a GET request.

> To call the content recognition API, you must include a signature in the request. For more information about the rule, see [Request Signature](https://intl.cloud.tencent.com/document/product/1045/33452).

## Request Syntax

```
GET /<ObjectKey>ci-process=sensitive-content-recognition&detect-type=<type> HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```


> Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)

## Request Content

Content-Recognition is a string in JSON format. Related parameters are described as follows:

| Parameter Name | Type | Required| Description |
| ----------- | ----- | ---- | ------------------------------------------------------------ |
| ObjectKey | String | Yes | The object file name, for example, picture.jpg. |
| type | String | Yes | The moderation type. The values of this parameter include porn (pornographic content recognition), terrorist (terrorism content recognition), politics (political content recognition), and ads (advertising content recognition). You can select multiple recognition types. For example, detect-type=porn,ads indicates that the image is moderated for both pornographic and advertising content. |

## Response
The content of the response body is described as follows:

| Parameter Name | Type | Description |
| ----------------- | --------- | ------------ |
| RecognitionResult | Container | Content recognition result |

The content of the RecognitionResult node:

| Parameter Name | Type | Description |
| ------------- | --------- | -------------- |
| PornInfo | Container | Pornographic content moderation information |
| TerroristInfo | Container | Terrorism content moderation information |
| PoliticsInfo | Container | Political content moderation information |
| AdsInfo | Container | Advertising content moderation information |

The content of PornInfo, TerroristInfo, PoliticsInfo, and AdsInfo:


| Parameter Name | Type | Description |
| -------- | ------ | ------------------------------------------------------------ |
| Code | Int | The error code. 0 indicates true, and other numbers indicate corresponding errors. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700). |
| HitFlag | Int | Whether the moderation category is hit. 0 indicates that it is not hit, and 1 indicates that it is hit. |
| Score | Int | The moderation score. A score within the range of 0-60 indicates that the image is normal; a score within the range of 60-90 indicates that the image may contain sensitive content; a score within the range of 90-100 indicates that the image definitely contains sensitive content. |
| Label | String | The tag of the recognized image. |


## Example

**Request**

```
GET /picture.jpg??ci-process=sensitive-content-recognition&detect-type=porn,politics HTTP/1.1
Host: examplebucket-1250000000.pic.ap-chengdu.myqcloud.com
Date: Tue, 03 Apr 2019 09:06:15 GMT
Authorization: XXXXXXXXXXXX
```

**Response**

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 645
Date: Tue, 03 Apr 2018 09:06:16 GMT
Status: 200 OK
x-cos-request-id: NWFjMzQ0MDZfOTBmYTUwXzZkZV8zMQ==

<RecognitionResult>
   <PornInfo>
      <Code>0</Code>
      <Msg>OK</Msg>
      <HitFlag>1</HitFlag>
      <Score>100</Score>
      <Label>xxx</Label>
   </PornInfo>
   <PoliticsInfo>
      <Code>0</Code>
      <Msg>OK</Msg>
      <HitFlag>0</HitFlag>
      <Score>10</Score>
      <Label>xx</Label>
   </PoliticsInfo>
</RecognitionResult>
```