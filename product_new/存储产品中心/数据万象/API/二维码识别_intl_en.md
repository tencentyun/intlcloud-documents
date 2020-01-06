## Description
During image upload, the request packet for QR code recognition is consistent with that of the simple upload API of COS, except that the image processing parameter `Pic-Operations` is added to the header of the request packet and `Host ` in the request is changed to the CI domain name.


## Request Syntax
```
PUT /<ObjectKey> HTTP/1.1 
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com 
Date: GMT Date 
Authorization: Auth String 
Pic-Operations: <PicOperations> 
```

>
- For more information on the simple upload API of COS, see [PUT Object Documentation](https://intl.cloud.tencent.com/document/product/436/7749).
> Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)


## Request Content 

`Pic-Operations` is a string in JSON format. Related parameters are described as follows:

| Parameter Name | Type | Required | Description |
| ----------- | ----- | ---- | ------------------------------------------------------------ |
| is_pic_info | Int | No | Whether to return the original image information. 0: no. 1: yes. The default value is 0. |
| rules | Array | No | Processing rules. One rule corresponds to one processing result (currently, a maximum of five rules are supported.) If this parameter is not specified, image processing is not performed. |


Parameters in rules (a JSON array) are described as follows:

| Parameter Name | Type | Required | Description |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| bucket | String | No | The destination bucket that stores the result. The format is BucketName-APPID. If this parameter is not specified, the result is stored in the current bucket by default. |
| fileid | String | No | Path of the file that stores the processing result. If this parameter starts with **/**, the result is stored in the specified folder; otherwise, the result is stored in the same directory as the original image file. |
| rule | String | Yes | The processing parameter. For more information, see the image processing API of CI. If the image needs to be processed according to a specified style, this parameter starts with **style/**, followed by a style name.<br>For example, if the style name is **test**, the value of the rule field is **style/test**. |


To use the QR code recognition feature, add the `QRcode` parameter to `rule` as follows:
```
QRcode/cover/<mode>
```

| Parameter | Type | Required | Description |
| --------- | ------- | ------ | ------------------------------------------------------------ |
| cover | Int | No | Whether the QR code cover feature is enabled. Valid values: 0 and 1. <li>0: QR code cover is disabled. <li>1: QR code cover is enabled.<br>After this feature is enabled, the recognized QR code is covered with a mosaic. The default value is 0. |


## Response 
The content of the response body is described as follows: 

| Parameter Name | Type | Description |
| ------------ | --------- | -------- |
| UploadResult | Container | Original image information |


The content of the UploadResult node: 

| Parameter Name | Type | Description |
| -------------- | --------- | ------------ |
| OriginalInfo | Container | Original image information |
| ProcessResults | Container | Image processing result |


The content of the OriginalInfo node: 

| Node Name | Type | Description |
| --------- | --------- | ------------ |
| Key | String | Name of the original image file |
| Location | String | Path of the image file |
| ImageInfo | Container | Original image information |


The content of the ImageInfo node: 

| Node Name | Type | Description |
| ----------- | ------ | ------------ |
| Format | String | Format |
| Width | Int | Image width |
| Height | Int | Image height |
| Quality | Int | Image quality |
| Ave | String | Image average tone |
| Orientation | Int | Image orientation |

The content of the ProcessResults node: 

| Node Name | Type | Description |
| -------- | --------- | ------------------ |
| Object | Container | Each image processing result |


The content of the Object node: 

| Node Name | Type | Description |
| -------------- | ------------- | ---------------------------------------------------------- |
| Key | String | File name |
| Location | String | Path of the image file |
| Format | String | Image format |
| Width | Int | Image width |
| Height | Int | Image height |
| Size | Int | Image size |
| Quality | Int | Image quality |
| codeStatus | Int | The result of QR code recognition. 0: No QR code is recognized. 1: A QR code is recognized. |
| QRcodeInfo | Container | QR code recognition results. There may be multiple results. |


The content of the QRcodeInfo node: 

| Node Name | Type | Description |
| -------------- | ------------- | ---------------------------------------------------------- |
| codeUrl | String | Content of the QR code, which may fail to be recognized |
| codelocation | Container | Location coordinates of the recognized QR code in the image |


The content of the codelocation node:

| Node Name | Type | Description |
| -------------- | ------------- | ---------------------------------------------------------- |
| point | Int | Coordinate point of the QR code |



## Sample 

**Request** 

```
PUT /picture.jpg HTTP/1.1 
Host: examplebucket-1250000000.pic.ap-chengdu.myqcloud.com 
Date: Tue, 03 Apr 2018 09:06:15 GMT 
Authorization: XXXXXXXXXXXX 
Pic-Operations: {"is_pic_info":1,"rules":[{"fileid":"test.jpg","rule":" QRcode/cover/1"}]} 
Content-Length: 64 

[Object] 
```

**Response packet**

```
HTTP/1.1 200 OK 
Content-Type: application/xml 
Content-Length: 645 
Date: Tue, 03 Apr 2018 09:06:16 GMT 
Status: 200 OK
x-cos-request-id: NWFjMzQ0MDZfOTBmYTUwXzZkZV8zMQ== 

<UploadResult>
  <OriginalInfo>
      <Key>picture.jpg</Key>
      <Location>examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/picture.jpg</Location>
      <ImageInfo>
        <Format>JPEG</Format>
        <Width>640</Width>
        <Height>427</Height>
        <Quality>100</Quality>
        <Ave>0xa18454</Ave>
        <Orientation>1</Orientation>
      </ImageInfo>
  </OriginalInfo>
  <ProcessResults>
      <Object>
        <Key>picture-2.jpg</Key>
        <Location>examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/picture-2.jpg</Location>
        <Format>png</Format>
        <Width>640</Width>
        <Height>427</Height>
        <Size>463092</Size>
        <Quality>100</Quality>
        <codeStatus>1</codeStatus>
        <QRcodeInfo>
          <codeUrl>xxxxxxxxxxxxx</codeUrl>
          <codelocation>
            <point>100,100</point>
            <point>100,200</point>
            <point>200,200</point>
            <point>200,100</point>
          </codelocation>
        </QRcodeInfo>
          <codeUrl>xxxxxxxxxxxxx</codeUrl>
          <codelocation>
            <point>1000,1000</point>
            <point>1000,2000</point>
            <point>2000,2000</point>
            <point>2000,1000</point>
          </codelocation>
      </Object>
  </ProcessResults>
</UploadResult>
```