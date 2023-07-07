## Overview

This document provides an overview of APIs and SDK code samples for blind watermarking.

| API | Description |
| ------------------------------------------ | -------------------------- |
| [Blind watermarking](https://www.tencentcloud.com/document/product/1045/43029) | Adds blind watermark to or extracts blind watermark from local image and uploads it to bucket. |

## Adding Blind Watermark

#### Feature description

You can add a blind watermark when uploading or downloading an object.

#### Sample: Adding a blind watermark during upload

[//]: # ".cssg-snippet-put-object-with-watermark"
```java
// The bucket name must contain `appid`.
// For the API description, visit https://cloud.tencent.com/document/product/436/46782.
String bucketName = "examplebucket-1250000000";

String key = "test.png";
File localFile = new File("E://test.png");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
PicOperations picOperations = new PicOperations();
picOperations.setIsPicInfo(1);
List<PicOperations.Rule> ruleList = new LinkedList<>();
PicOperations.Rule rule = new PicOperations.Rule();
rule.setBucket(bucketName);
rule.setFileId("test-watermark.png");
rule.setRule("watermark/3/type/3/text/dGVuY2VudCBjbG91ZA==");
ruleList.add(rule);
picOperations.setRules(ruleList);
putObjectRequest.setPicOperations(picOperations);
try {
    PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
    CIUploadResult ciUploadResult = putObjectResult.getCiUploadResult();
    System.out.println(putObjectResult.getRequestId());
    System.out.println(ciUploadResult.getOriginalInfo().getEtag());
    for(CIObject ciObject:ciUploadResult.getProcessResults().getObjectList()) {
        System.out.println(ciObject.getLocation());
    }
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```

#### Parameter description

The `PicOperations` class is used to record image operations. Its main members are as described below:

| Member | Description | Type |
| --------- | ------------------------------------------------------------ | ---- |
| isPicInfo | Whether to return the input image information. Valid values: 0 (no), 1 (yes). Default value: 0.    | int  |
| rules       |  Processing rules (up to five rules are supported). Each rule corresponds to one processing result. If this parameter is not specified, images will not be processed. | List |

#### Response parameter description

The `CIUploadResult` class is used to return the image processing result. Its main members are as described below:

| Member | Description | Type |
| -------------- | ------------ | -------------- |
| originalInfo   | Input image information     | OriginalInfo   |
| processResults | Image processing result | ProcessResults |

  The `OriginalInfo` class is used to record the input image information. Its main members are as described below:

| Member | Description | Type |
| --------- | ---------------------------------------------------------- | --------- |
| key       | Name of the input image                                                 | String    |
| location  | Image path                                                   | String    |
| imageInfo | Input image information                                               | ImageInfo |


The `ImageInfo` class is used to record the input image information. Its main members are as described below:

| Member | Description | Type |
| ----------- | ------------ | ------- |
| format      | Format | String  |
| width       | Image width | Integer |
| height      | Image height | Integer |
| quality     | Image quality     | Integer |
| ave         | Image average hue   | String  |
| orientation | Image rotation angle | Integer |

The `ProcessResults` class is used to record the image processing results. Its main members are as described below:

| Member | Description | Type |
| ---------- | ------------------ | ---- |
| objectList | Processing result of each image | List |

The `CIObject` class is used to record the processing result of a single image. Its main members are as described below:

| Member | Description | Type |
| -------------- | -------------------------- | ------- |
| key            | Filename                     | String  |
| location       | Image path                   | String  |
| format         | Image format  | String  |
| width          | Image width  | Integer |
| height         | Image height | Integer |
| size           | Image size | Integer |
| quality        | Image quality                   | Integer |



#### Sample: Adding a blind watermark during download

[//]: # ".cssg-snippet-download-object-with-watermark"
```java
GetObjectRequest getObj = new GetObjectRequest(bucketName, key);
// The following are blind watermarking rules. For more information, see the API description of CI.
String rule = "watermark/3/type/3/text/dGVuY2VudCBjbG91ZA==";
getObj.putCustomQueryParameter(rule, null);

cosClient.getObject(getObj);
```


## Extracting Blind Watermark

The following example shows how to extract a blind watermark from an image.

#### Sample code

[//]: # ".cssg-snippet-get-object-watermark-status"
```java
String bucketName = "examplebucket-1250000000";
String key = "qrcode-watermark.png";
File localFile = new File("E://qrcode-watermark.png");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
PicOperations picOperations = new PicOperations();
picOperations.setIsPicInfo(1);
List<PicOperations.Rule> ruleList = new LinkedList<>();
PicOperations.Rule rule = new PicOperations.Rule();
rule.setBucket(bucketName);
rule.setFileId("qrcode-watermark-extract.png");
rule.setRule("watermark/4/type/2/image/aHR0cDovL2V4YW1wbGVidWNrZXQtMTI1MDAwMDAwMC5jb3MuYXAtZ3Vhbmd6aG91Lm15cWNsb3VkLmNvbS9zaHVpeWluLnBuZw==");
ruleList.add(rule);
picOperations.setRules(ruleList);
putObjectRequest.setPicOperations(picOperations);
try {
    PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
    CIUploadResult ciUploadResult = putObjectResult.getCiUploadResult();
    System.out.println(putObjectResult.getRequestId());
    System.out.println(ciUploadResult.getOriginalInfo().getEtag());
    for(CIObject ciObject:ciUploadResult.getProcessResults().getObjectList()) {
        System.out.println(ciObject.getLocation());
        System.out.println(ciObject.getWatermarkStatus());
    }
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```
#### Parameter description

The `PicOperations` class is used to record image operations. Its main members are as described below:

| Member | Description | Type |
| --------- | ------------------------------------------------------------ | ---- |
| isPicInfo | Whether to return the input image information. Valid values: 0 (no), 1 (yes). Default value: 0.    | int  |
| rules       |  Processing rules (up to five rules are supported). Each rule corresponds to one processing result. If this parameter is not specified, images will not be processed. | List |

#### Response parameter description

The `CIUploadResult` class is used to return the image processing result. Its main members are as described below:

| Member | Description | Type |
| -------------- | ------------ | -------------- |
| originalInfo   | Input image information     | OriginalInfo   |
| processResults | Image processing result | ProcessResults |

  The `OriginalInfo` class is used to record the input image information. Its main members are as described below:

| Member | Description | Type |
| --------- | ---------------------------------------------------------- | --------- |
| key       | Name of the input image                                                 | String    |
| location  | Image path                                                   | String    |
| imageInfo | Input image information                                               | ImageInfo |


The `ImageInfo` class is used to record the input image information. Its main members are as described below:

| Member | Description | Type |
| ----------- | ------------ | ------- |
| format      | Format | String  |
| width       | Image width | Integer |
| height      | Image height | Integer |
| quality     | Image quality     | Integer |
| ave         | Image average hue   | String  |
| orientation | Image rotation angle | Integer |

The `ProcessResults` class is used to record the image processing results. Its main members are as described below:

| Member | Description | Type |
| ---------- | ------------------ | ---- |
| objectList | Processing result of each image | List |

The `CIObject` class is used to record the processing result of a single image. Its main members are as described below:

| Member | Description | Type |
| --------------- | ------------------------------------------------------------ | ------- |
| key             | Filename                                                       | String  |
| location        | Image path                                                     | String  |
| format          | Image format                                                     | String  |
| width           | Image width                                                     | Integer |
| height          | Image height                                                     | Integer |
| size            | Image size                                                     | Integer |
| quality         | Image quality                                                     | Integer |
| watermarkStatus | This parameter will be returned if `type` is set to `2`, indicating the confidence of the extracted watermark. Value range: 0–100. If the value is above 75, there is a confirmed blind watermark. If the value is between 60 and 75, there is a suspected blind watermark. If the value is below 60, no blind watermark is extracted. | Integer |
