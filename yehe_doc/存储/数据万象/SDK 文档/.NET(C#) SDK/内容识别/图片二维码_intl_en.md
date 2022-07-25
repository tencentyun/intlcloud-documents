
## Overview

This document provides an overview of APIs and SDK code samples for image QR codes.

| API | Description    |
| ------------------------------------------------------------ | ----------------------------------------- |
| [QR code recognition](https://intl.cloud.tencent.com/document/product/1045/47945) | Recognizes the location and content of valid QR codes in an image, outputs the text information (URL or text) contained in the QR codes, and pixelates the recognized QR codes. |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see the [API documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## QR Code Recognition

The QR code recognition feature recognizes the location and content of valid QR codes in an image, outputs the text information (URL or text) contained in the QR codes, and pixelates the recognized QR codes.


### Recognizing QR code during upload

#### Feature description

The QR code recognition feature can recognize QR codes when files are uploaded.

#### Sample code

[//]: # ".cssg-snippet-upload-with-QRcode-recognition"
```cs
PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);

JObject o = new JObject();
// Do not return the input image
o["is_pic_info"] = 1;
JArray rules = new JArray();
JObject rule = new JObject();
rule["bucket"] = bucket;
rule["fileid"] = "qrcode.jpg";
// Processing parameters. For rules, visit https://cloud.tencent.com/document/product/436/54070.
rule["rule"] = "QRcode/cover/<mode>";
rules.Add(rule);
o["rules"] = rules;

string ruleString = o.ToString(Formatting.None);
request.SetRequestHeader("Pic-Operations", ruleString);
// Execute the request
PutObjectResult result = cosXml.PutObject(request);
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/QrcodeRecognition.cs).
>

### Recognizing QR code during download

#### Feature description

The QR code recognition feature can recognize QR codes when files are downloaded.

#### Sample code

[//]: # ".cssg-snippet-download-with-qrcode-recognition"
```cs
// Pixelate the recognized QR code. Valid values: 0 (no), 1 (yes). Default value: 0.
QRCodeRecognitionRequest request = new QRCodeRecognitionRequest(bucket, key, 0);

QRCodeRecognitionResult result = cosXml.QRCodeRecognition(request);
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/QrcodeRecognition.cs).
>

