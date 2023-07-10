## Overview

The following example shows how to automatically process an image when you upload it to COS.

When the image is uploaded successfully, COS(Cloud Object Storage) will save both the input and output images. You can later obtain the processing results using a general download request.

## Persistent Image Processing upon Upload

#### Sample code

[//]: # ".cssg-snippet-upload-with-pic-operation"
```java
  // The bucket name must contain "appid".
// For the API description, please see https://cloud.tencent.com/document/product/436/54050
String bucketName = "examplebucket-1250000000";

String key = "test.jpg";
File localFile = new File("E://test.jpg");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
PicOperations picOperations = new PicOperations();
picOperations.setIsPicInfo(1);
// Add image processing rules.
List<PicOperations.Rule> ruleList = new LinkedList<>();
PicOperations.Rule rule1 = new PicOperations.Rule();
rule1.setBucket(bucketName);
rule1.setFileId("test-1.jpg");
rule1.setRule("imageMogr2/rotate/90");
ruleList.add(rule1);
PicOperations.Rule rule2 = new PicOperations.Rule();
rule2.setBucket(bucketName);
rule2.setFileId("test-2.jpg");
rule2.setRule("imageMogr2/rotate/180");
ruleList.add(rule2);
picOperations.setRules(ruleList);
putObjectRequest.setPicOperations(picOperations);
try {
    PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
    CIUploadResult ciUploadResult = putObjectResult.getCiUploadResult();
    System.out.println(putObjectResult.getRequestId());
    System.out.println(ciUploadResult.getOriginalInfo().getEtag());
    for(CIObject ciObject:ciUploadResult.getProcessResults().getObjectList()) {
        System.out.println(ciObject.getLocation());
        System.out.println(ciObject.getEtag());
    }
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```

#### Parameter description

The `PicOperations` class is used to record image operations. Its members are described as follows:

| Member | Description | Type |
| --------- | ------------------------------------------------------------ | ---- |
| isPicInfo | Whether to return the input image information. <br>`0`: No (default)<br>`1`: Yes | int |
| rules | Processing rules (up to 5 rules are supported). Each rule corresponds to one processing result. If this parameter is not specified, images will not be processed. | List |

#### Response parameters

The `CIUploadResult` class is used to return the image processing results. Its members are described as follows:

| Member | Description | Type |
| -------------- | ------------ | -------------- |
| originalInfo   | Input image information | OriginalInfo   |
| processResults | Processing results | ProcessResults |

  The `OriginalInfo` class is used to record the input image information. Its members are described as follows:

| Member | Description | Type |
| --------- | ---------------------------------------------------------- | --------- |
| key       | Name of the input image      | String    |
| location  | Location of the input image          | String    |
| imageInfo | Input image information        | ImageInfo |
| etag      | ETag of the input image. If the output image overwrites the input image, the value of `etag` will be that of the output image | String    |

The `ImageInfo` class is used to record the input image information. Its members are described as follows:

| Member | Description | Type |
| ----------- | ------------ | ------- |
| format      | Format | String  |
| width       | Image width | Integer |
| height      | Image height | Integer |
| quality     | Image quality | Integer |
| ave         | Average hue of the image | String  |
| orientation | Rotation angle of the image | Integer |

The `ProcessResults` class is used to record the image processing results. Its members are described as follows:

| Member | Description | Type |
| ---------- | ------------------ | ---- |
| objectList | Processing results of each image | List |

The `CIObject` class is used to record the processing result of a single image. Its members are described as follows:

| Member | Description | Type |
| -------------- | -------------------------- | ------- |
| key  | Filename | String  |
| location       | Location of the image | String  |
| format         | Image format  | String  |
| width          | Image width  | Integer |
| height         | Image height | Integer |
| size           | Image size | Integer |
| quality        | Image quality | Integer |
| etag | ETag of the output image | String |



## Processing an In-Cloud Image

The following example shows how to process an in-cloud image and store the processing result in COS.

#### Sample code

[//]: # ".cssg-snippet-process-with-pic-operation"
```java
String bucketName = "examplebucket-1250000000";
String key = "test.jpg";
ImageProcessRequest imageReq = new ImageProcessRequest(bucketName, key);

PicOperations picOperations = new PicOperations();
picOperations.setIsPicInfo(1);
List<PicOperations.Rule> ruleList = new LinkedList<>();
PicOperations.Rule rule1 = new PicOperations.Rule();
rule1.setBucket(bucketName);
rule1.setFileId("test-1.jpg");
rule1.setRule("imageMogr2/rotate/90");
ruleList.add(rule1);
PicOperations.Rule rule2 = new PicOperations.Rule();
rule2.setBucket(bucketName);
rule2.setFileId("test-2.jpg");
rule2.setRule("imageMogr2/rotate/180");
ruleList.add(rule2);
picOperations.setRules(ruleList);

imageReq.setPicOperations(picOperations);

CIUploadResult result = cosClient.processImage(imageReq);
result.getProcessResults();
result.getOriginalInfo();

try {
    CIUploadResult ciUploadResult = cosClient.processImage(imageReq);
    System.out.println(ciUploadResult.getOriginalInfo().getEtag());
    for(CIObject ciObject:ciUploadResult.getProcessResults().getObjectList()) {
        System.out.println(ciObject.getLocation());
        System.out.println(ciObject.getEtag());
    }
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```
