## Overview

This document provides an overview of APIs and SDK code samples for image tagging.

| API | Description |
| ------------- |  ---------------------- |
| Tagging image | Recognizes tags in an image stored in COS. |

## Image Tagging

#### Feature description

The image tagging feature recognizes tags in images stored in COS by using the persistent processing API of CI and returns tags with a high confidence. Image tagging requests are `GET` requests and need to carry a signature.

#### Method prototype

```java
ImageLabelResponse getImageLabel(ImageLabelRequest request);
```


#### Sample request

```java
//1. Create a job request object
ImageLabelRequest request = new ImageLabelRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("demo-123456789");
request.setObjectKey("1.png");
//3. Call the API to get the job response object
ImageLabelResponse response = client.getImageLabel(request);
```


#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| bucketName | Request | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| objectKey | Request | Location of the image in the bucket | String    | Yes   |

#### Response description

- Success: An `ImageLabelResponse` instance is returned upon success, which contains the result.
- Failure: An error (such as the bucket does not exist) occurs, reporting the `CosClientException` or `CosServiceException` exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
